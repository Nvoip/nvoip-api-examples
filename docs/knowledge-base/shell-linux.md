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
./examples/create-access-token.sh
./examples/get-balance.sh
./examples/create-call.sh
./examples/list-whatsapp-templates.sh
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS, torpedo de voz e saldo.
