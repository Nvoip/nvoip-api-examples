# Como testar a API Nvoip v3 pelo Postman

Importe a [coleção e o environment oficiais derivados do OpenAPI](https://github.com/Nvoip/nvoip-api-v3/tree/main/docs/postman). A fonte canônica é o OpenAPI da v3; a coleção deve ser regenerada pelos scripts do repositório quando o contrato mudar.

## Ambiente local

Use `baseUrl=https://api.nvoip.com.br/v3` e `authBaseUrl=https://api.nvoip.com.br/auth`. Preencha `oauthClientId`, `oauthClientCredential` e `oauthBearer` apenas no environment privado/local; não publique valores de credenciais no workspace.

Em `POST {{authBaseUrl}}/oauth2/token`, use formulário com `grant_type=client_credentials`, `client_id` e `client_secret`. Para agir em nome de um usuário, use o helper OAuth 2.0 com Authorization Code e PKCE `S256`, redirect URI cadastrado e consentimento.

## Consulta inicial

Execute a emissão de token e depois `GET {{baseUrl}}/balance` com `Authorization: Bearer {{oauthBearer}}`. Confira HTTP 200 e a conta de teste. A v2 não deve ser a URL base da nova integração.

Operações de envio, compra de número e alteração de dados devem ficar fora do runner padrão. As variáveis de destino e de conta gerenciada ficam vazias até um cenário autorizado. Confirme as permissões de escopo por recurso.

Veja o [guia de migração](../migration-v2-v3.md). A disponibilidade da coleção pública deve ser conferida após a publicação; importar um arquivo revisado localmente não atualiza o Postman público.
