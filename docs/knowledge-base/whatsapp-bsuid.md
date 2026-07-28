# Como enviar template WhatsApp para telefone ou BSUID

A API Nvoip mantém o campo `destination` para integrações existentes que enviam
para telefone e adiciona o objeto `recipient` para destinatários tipados.

Informe exatamente uma das duas formas:

```json
{
  "idTemplate": "template-masked",
  "destination": "5511999999999",
  "instance": "instance-masked",
  "language": "pt_BR"
}
```

```json
{
  "idTemplate": "template-masked",
  "recipient": {
    "type": "bsuid",
    "value": "US.MASKED_BSUID_001"
  },
  "instance": "instance-masked",
  "language": "pt_BR"
}
```

Para um parent BSUID, use `type: "parent_bsuid"` e um valor opaco, como
`PARENT.MASKED_BSUID_001`. Também é possível usar `type: "phone"` com o número
em `recipient.value`.

## Regras de validação

- Não combine `destination` e `recipient`.
- `destination` e `recipient.type=phone` aceitam somente telefone com 8 a 20
  dígitos e `+` inicial opcional.
- Não use `@username`. O nome público do WhatsApp não é um identificador de
  envio; obtenha o BSUID apropriado no fluxo oficial da Meta.
- Não coloque BSUID em campos de telefone. Trate BSUID e parent BSUID como
  valores opacos, sem inferir telefone, país ou identidade.
- Abertura de atendimento e reply Flow dependem de telefone e não estão
  disponíveis para BSUID.
- Contas de clientes de revendedores não podem disparar WhatsApp por este
  endpoint.

## Resposta e erros

Na API V3, a resposta pode incluir os identificadores que a Meta efetivamente
fornecer:

```json
{
  "templateId": "template-masked",
  "message_id": "wamid.MASKED",
  "user_id": "US.MASKED_BSUID_001"
}
```

`user_id` e `wa_id` são opcionais; a API não inventa um valor quando a Meta o
omite. A API V2 mantém a resposta `204 No Content` por compatibilidade.

O erro Meta 131062 é mapeado para o código público estável
`WHATSAPP_BSUID_AUTH_TEMPLATE_UNSUPPORTED`. Ele indica especificamente que o
template de autenticação escolhido exige telefone e não pode ser enviado ao
BSUID.

## Compatibilidade dos templates

Segundo a documentação da Meta, mensagens para BSUID usam
`recipient_type: "individual"` e o campo `to`, que aceita telefone ou BSUID.
Templates de autenticação one-tap, zero-tap e copy-code não são compatíveis com
BSUID. Valide o tipo do template antes do envio.

Referência: [Business-scoped user IDs — Meta](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids).

## Mapeamento para Make, Zapier e n8n

Conectores devem exibir um seletor `phone`, `bsuid` ou `parent_bsuid` e montar
somente um destes formatos:

- `phone`: `destination: "<telefone>"`;
- `bsuid`: `recipient: { "type": "bsuid", "value": "<valor opaco>" }`;
- `parent_bsuid`: `recipient: { "type": "parent_bsuid", "value": "<valor opaco>" }`.

O conector não deve manter um campo `destination` oculto quando `recipient`
estiver selecionado. Também deve preservar `user_id`/`wa_id` na saída e expor o
`code` dos erros estáveis sem substituir a mensagem por texto do provedor.
