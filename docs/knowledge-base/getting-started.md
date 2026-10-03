# Primeiros passos com a API Nvoip v3

Crie um cliente OAuth na tela Desenvolvedor do Painel, com os escopos necessários e `client_credentials` habilitado. Guarde `client_id` e `client_secret` apenas no backend ou no cofre da sua aplicação.

## Autenticação

A URL da API é `https://api.nvoip.com.br/v3`. A emissão do token é separada:

```http
POST https://api.nvoip.com.br/auth/oauth2/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=SEU_CLIENT_ID&client_secret=SEU_CLIENT_SECRET
```

O corpo deve ser codificado como formulário, incluindo caracteres especiais das credenciais. O token recebido vai em `Authorization: Bearer <token>`. Respeite `expires_in`: `client_credentials` não promete refresh token; obtenha um novo access token quando necessário.

## Primeira consulta

Comece com `GET /v3/balance`, usando uma conta própria de teste. Confirme HTTP 200 e o saldo esperado sem registrar o token. Para outras operações, consulte o [contrato OpenAPI](https://github.com/Nvoip/nvoip-api-v3/blob/main/docs/openapi/openapi.yaml).

Instale a versão do SDK que suporta a v3 após sua publicação. Exemplos de envio exigem destinatário, template, saldo e permissão próprios; não execute um runner com operações de envio por padrão.

Veja o [guia de migração](../migration-v2-v3.md), os [SDKs por linguagem](README.md) e o [Postman](postman.md).
