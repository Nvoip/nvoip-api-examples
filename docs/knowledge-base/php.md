# Como integrar a API Nvoip com PHP

Repositório: https://github.com/Nvoip/nvoip-php

Pacote: https://packagist.org/packages/nvoip/nvoip-php

## Instalação

```bash
composer require nvoip/nvoip-php:^3.0
```

## Configuração

Use OAuth `client_credentials` no backend, com um cliente criado na tela Desenvolvedor e os escopos da operação. A API usa `https://api.nvoip.com.br/v3`; o token é emitido em `https://api.nvoip.com.br/auth/oauth2/token`. Guarde o token recebido em `NVOIP_ACCESS_TOKEN`.

Antes de instalar, confira se a versão que usa a v3 já foi publicada; os PRs não atualizam automaticamente os registries.

```bash
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
