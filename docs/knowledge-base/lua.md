# Como integrar a API Nvoip com Lua

Repositório: https://github.com/Nvoip/nvoip-lua

Pacote: https://luarocks.org/modules/nvoip/nvoip

## Instalação

```bash
luarocks install nvoip
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
lua examples/create_access_token.lua
lua examples/get_balance.lua
lua examples/create_call.lua
lua examples/list_whatsapp_templates.lua
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.
