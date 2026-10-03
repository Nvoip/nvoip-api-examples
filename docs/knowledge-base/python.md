# Como integrar a API Nvoip com Python

Repositório: https://github.com/Nvoip/nvoip-python

Pacote: https://pypi.org/project/nvoip/

## Instalação

```bash
pip install nvoip==3.0.1
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
python3 examples/create_access_token.py
python3 examples/get_balance.py
python3 examples/create_call.py
python3 examples/list_whatsapp_templates.py
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.
