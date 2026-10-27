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

Autentique as consultas com o access token OAuth 2.0 no header padrão ou com
uma chave API v3 no header `X-Nvoip-Api-Key`.

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
  "name": "Status de mensagens",
  "url": "https://example.com/nvoip/webhooks",
  "events": ["sms.status.updated", "whatsapp.status.updated"],
  "protection": {
    "authType": "basic",
    "username": "nvoip-webhook",
    "secret": "<senha-forte>",
    "allowedIpRanges": ["<IP_PUBLICO>/32"]
  }
}
```

Autentique a gestão com OAuth 2.0 ou com uma chave API v3 criada em
`/developer`. A chave precisa conter `sms:query` ou `whatsapp:send`, de acordo
com os eventos usados pela integração.

O destino precisa ser HTTPS público na porta 443. A resposta contém um
`secret` somente na criação; salve-o em um cofre de segredos. Listagens e
alterações posteriores não o devolvem.

O HMAC da Nvoip permanece sempre ativo. A proteção opcional do destino aceita
um modo por assinatura: `basic`, `bearer` ou `header`. No modo `header`, use um
nome `X-*` que não seja reservado pela Nvoip. `allowedIpRanges` limita os IPs
públicos aos quais o dispatcher pode se conectar depois de resolver a URL; não
é a lista de IPs de saída da Nvoip. Senhas e tokens são cifrados, nunca aparecem
na listagem e não devem ser colocados na query string da URL.

Use `GET /v3/webhooks` para listar e `PUT /v3/webhooks/{id}` para alterar nome,
URL, eventos e proteção. Ao editar, omita `protection.secret` para manter o
segredo atual. Os controles de estado são:

- `POST /v3/webhooks/{id}/pause`: pausa novas entregas;
- `POST /v3/webhooks/{id}/resume`: retoma apenas eventos futuros;
- `POST /v3/webhooks/{id}/deactivate`: desativa definitivamente.

Uma assinatura inativa não pode ser editada nem retomada. Eventos ocorridos
durante a pausa não são enviados depois.

A assinatura começa a valer na criação: eventos históricos não são enviados.
A credencial precisa ter `sms:query` ou `whatsapp:send`, de acordo com o canal
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
