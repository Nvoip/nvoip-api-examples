# Primeiros passos com a API Nvoip

Este guia mostra o fluxo mínimo para começar a integrar a API v2 da Nvoip.

## Antes de começar

Você precisa acessar o painel Nvoip e obter:

- `numbersip`
- `user-token`
- `client_id`
- `client_secret`

Use OAuth para integrações comerciais. Evite colocar credenciais no frontend, em repositórios públicos ou em apps mobile sem backend.

## Fluxo recomendado

1. Gere um `access_token` pelo endpoint `/oauth/token`.
2. Use `Authorization: Bearer ACCESS_TOKEN` nas chamadas da API.
3. Renove o token antes de expirar.
4. Use SDKs ou exemplos por linguagem para reduzir erro de integração.

## Variáveis padrão usadas nos exemplos

```bash
export NVOIP_NUMBERSIP="seu_numbersip"
export NVOIP_USER_TOKEN="seu_user_token"
export NVOIP_OAUTH_CLIENT_ID="seu_client_id"
export NVOIP_OAUTH_CLIENT_SECRET="seu_client_secret"
export NVOIP_CALLER="1049"
export NVOIP_TARGET_NUMBER="11999999999"
```

## Principais recursos

- Autenticação OAuth
- Chamada de saída
- OTP por SMS, voz ou email
- SMS
- WhatsApp templates
- Consulta de saldo

## Onde baixar exemplos

Use o índice oficial em https://github.com/Nvoip/nvoip-api-examples.
