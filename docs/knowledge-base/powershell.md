# Como integrar a API Nvoip com PowerShell

Repositório: https://github.com/Nvoip/nvoip-powershell

Pacote: https://www.powershellgallery.com/packages/Nvoip

## Instalação

```powershell
Install-Module Nvoip -RequiredVersion 1.0.0 -Scope CurrentUser
```

## Configuração

Use OAuth `client_credentials` no backend, com um cliente criado na tela Desenvolvedor e os escopos da operação. A API usa `https://api.nvoip.com.br/v3`; o token é emitido em `https://api.nvoip.com.br/auth/oauth2/token`. Guarde o token recebido em `NVOIP_ACCESS_TOKEN`.

Antes de instalar, confira se a versão que usa a v3 já foi publicada; os PRs não atualizam automaticamente os registries.

```powershell
$env:NVOIP_OAUTH_CLIENT_ID = "seu_client_id"
$env:NVOIP_OAUTH_CLIENT_SECRET = "seu_client_secret"
$env:NVOIP_CALLER = "1049"
$env:NVOIP_TARGET_NUMBER = "11999999999"
```

## Primeiros testes

```powershell
./examples/create-access-token.ps1
./examples/get-balance.ps1
./examples/create-call.ps1
./examples/list-whatsapp-templates.ps1
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.
