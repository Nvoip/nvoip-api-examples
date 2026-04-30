# Como integrar a API Nvoip com Ruby

Repositório: https://github.com/Nvoip/nvoip-ruby

Pacote: https://rubygems.org/gems/nvoip

## Instalação

```bash
gem install nvoip
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
ruby examples/create_access_token.rb
ruby examples/get_balance.rb
ruby examples/create_call.rb
ruby examples/list_whatsapp_templates.rb
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.
