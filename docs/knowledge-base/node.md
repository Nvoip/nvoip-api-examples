# Como integrar a API Nvoip com Node.js

Repositório: https://github.com/Nvoip/nvoip-node

Pacote: https://www.npmjs.com/package/nvoip-node

## Instalação

```bash
npm install nvoip-node
```

## Configuração

```bash
export NVOIP_NUMBERSIP="seu_numbersip"
export NVOIP_USER_TOKEN="seu_user_token"
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
