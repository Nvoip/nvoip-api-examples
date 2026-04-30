# Como integrar a API Nvoip com PowerShell

Repositório: https://github.com/Nvoip/nvoip-powershell

Pacote: https://www.powershellgallery.com/packages/Nvoip

## Instalação

```powershell
Install-Module Nvoip -Scope CurrentUser
```

## Configuração

```powershell
$env:NVOIP_NUMBERSIP = "seu_numbersip"
$env:NVOIP_USER_TOKEN = "seu_user_token"
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
