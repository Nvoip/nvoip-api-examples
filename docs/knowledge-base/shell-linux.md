# Como integrar a API Nvoip com Shell/Linux

Repositório: https://github.com/Nvoip/nvoip-shell

Homebrew: https://github.com/Nvoip/homebrew-tap

## Instalação via Homebrew

```bash
brew tap Nvoip/tap
brew install nvoip-shell
```

## Uso direto por clone

```bash
git clone https://github.com/Nvoip/nvoip-shell.git
cd nvoip-shell
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
./examples/create-access-token.sh
./examples/get-balance.sh
./examples/create-call.sh
./examples/list-whatsapp-templates.sh
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS, torpedo de voz e saldo.
