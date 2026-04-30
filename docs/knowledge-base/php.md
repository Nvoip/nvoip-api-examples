# Como integrar a API Nvoip com PHP

Repositório: https://github.com/Nvoip/nvoip-php

Pacote: https://packagist.org/packages/nvoip/nvoip-php

## Instalação

```bash
composer require nvoip/nvoip-php
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
php examples/create-access-token.php
php examples/create-call.php
php examples/send-sms.php
php examples/list-whatsapp-templates.php
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.
