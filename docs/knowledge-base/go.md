# Como integrar a API Nvoip com Go

Repositório: https://github.com/Nvoip/nvoip-go

Pacote: https://pkg.go.dev/github.com/Nvoip/nvoip-go

## Instalação

```bash
go get github.com/Nvoip/nvoip-go
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
go run ./cmd/create-access-token
go run ./cmd/get-balance
go run ./cmd/create-call
go run ./cmd/list-whatsapp-templates
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.
