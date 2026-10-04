# Como integrar a API Nvoip com Node.js

Repositório: https://github.com/Nvoip/nvoip-node

Pacote: https://www.npmjs.com/package/nvoip-node

## Instalação

```bash
npm install nvoip-node@3.0.0
```

## Configuração

Use OAuth `client_credentials` no backend, com um cliente criado na tela Desenvolvedor e os escopos da operação. A API usa `https://api.nvoip.com.br/v3`; o token é emitido em `https://api.nvoip.com.br/auth/oauth2/token`. Guarde o token recebido em `NVOIP_ACCESS_TOKEN`.

A versão 3.0.0 está disponível no npm e contém a migração para a v3 e OAuth.

```bash
export NVOIP_OAUTH_CLIENT_ID="seu_client_id"
export NVOIP_OAUTH_CLIENT_SECRET="seu_client_secret"
export NVOIP_CALLER="1049"
export NVOIP_TARGET_NUMBER="11999999999"
```

## Primeiros testes

```bash
npm run auth:token
npm run balance
npm run call:create
npm run wa:list
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.

## Disponibilidade da versão v3

A versão 3.0.0 está [disponível no npm](https://www.npmjs.com/package/nvoip-node/v/3.0.0). Instale essa versão para usar o caminho v3/OAuth descrito aqui.
