# Como integrar a API Nvoip com Python

Repositório: https://github.com/Nvoip/nvoip-python

Pacote: https://pypi.org/project/nvoip/

## Instalação

```bash
pip install nvoip
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
python3 examples/create_access_token.py
python3 examples/get_balance.py
python3 examples/create_call.py
python3 examples/list_whatsapp_templates.py
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.
