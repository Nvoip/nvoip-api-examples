# Status de entrega de SMS e WhatsApp por webhook

O retorno HTTP do envio confirma somente que a Nvoip aceitou ou enfileirou a
mensagem. Ele não confirma que a operadora ou o WhatsApp entregou o conteúdo ao
destinatário.

Guarde o `messageId` retornado pelo envio. Ele é estável, não contém o ID
incremental interno e pode ser usado como fallback de consulta:

```http
GET /v3/sms/messages/{messageId}
GET /v3/wa/messages/{messageId}
```

Autentique as consultas com o access token OAuth 2.0 no header padrão.

Os campos têm papéis diferentes:

- `submissionStatus`: aceite inicial pela Nvoip/provedor;
- `deliveryStatus`: último estado assíncrono persistido;
- `providerStatus`: estado bruto recebido do provedor;
- `finalStatus`: indica que não se espera outra transição. No WhatsApp,
  `delivered` ainda pode evoluir para `read`.

## Criar uma assinatura

```http
POST /v3/webhooks
Content-Type: application/json

{
  "url": "https://example.com/nvoip/webhooks",
  "events": ["sms.status.updated", "whatsapp.status.updated"]
}
```

Autentique a criação com o access token OAuth 2.0 no header padrão.

O destino precisa ser HTTPS público na porta 443. A resposta contém um
`secret` somente na criação; salve-o em um cofre de segredos. Listagens e
alterações posteriores não o devolvem.

Use `GET /v3/webhooks` para listar, `PUT /v3/webhooks/{id}` para alterar URL e
eventos e `POST /v3/webhooks/{id}/deactivate` para interromper novas entregas.
A assinatura começa a valer na criação: eventos históricos não são enviados.
O token OAuth precisa ter `sms:query` ou `whatsapp:send`, de acordo com o canal
integrado.

## Validar a assinatura

Cada entrega contém `X-Nvoip-Event-Id`, `X-Nvoip-Timestamp` e
`X-Nvoip-Signature: v1=<HMAC-SHA256>`. Calcule o HMAC sobre
`<timestamp>.<corpo bruto>`. Não serialize o JSON novamente. Compare em tempo
constante e recuse timestamps antigos.

```js
import crypto from "node:crypto";

export function verifyNvoipWebhook(rawBody, headers, secret) {
  const timestamp = String(headers["x-nvoip-timestamp"] || "");
  const received = String(headers["x-nvoip-signature"] || "").replace(/^v1=/, "");
  const age = Math.abs(Math.floor(Date.now() / 1000) - Number(timestamp));
  if (!Number.isFinite(age) || age > 300) return false;
  if (!/^[0-9a-f]{64}$/.test(received)) return false;

  const expected = crypto.createHmac("sha256", secret)
    .update(`${timestamp}.${rawBody}`).digest("hex");
  if (received.length !== expected.length) return false;
  return crypto.timingSafeEqual(Buffer.from(received), Buffer.from(expected));
}
```

A entrega é **at least once**: responda `2xx` rapidamente e deduplique pelo
`eventId`. Em timeout ou resposta não `2xx`, a Nvoip tenta novamente com
backoff e encerra a tentativa automática após oito falhas. Não presuma ordenação global entre mensagens; para uma mensagem,
compare o estado e `occurredAt` antes de atualizar seu sistema.

```json
{
  "schemaVersion": "1",
  "eventId": "aaaaaaaa-bbbb-4ccc-8ddd-eeeeeeeeeeee",
  "eventType": "sms.status.updated",
  "messageId": "11111111-2222-4333-8444-555555555555",
  "channel": "sms",
  "previousStatus": "accepted",
  "deliveryStatus": "delivered",
  "providerStatus": "DELIVERED",
  "reason": null,
  "occurredAt": "2026-10-26T20:00:00Z"
}
```
