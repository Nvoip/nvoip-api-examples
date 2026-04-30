# Como integrar a API Nvoip com .NET

Repositório: https://github.com/Nvoip/nvoip-dotnet

Pacote: https://www.nuget.org/packages/Nvoip

## Instalação

```bash
dotnet add package Nvoip
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
dotnet run --project examples/Nvoip.Examples
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.
