# Como testar a API Nvoip pelo Postman

O Postman complementa a documentação do Apiary. O Apiary explica a referência da API; o Postman permite executar requisições prontas com variáveis.

## Abrir a collection

Acesse o workspace público:

https://nvoip-api.postman.co/workspace/e671d01f-168a-4c38-8d0e-c217229dd61a/team-quickstart

## Configurar ambiente

Crie ou duplique um environment e preencha:

```text
base_url=https://api.nvoip.com.br/v2
numbersip=seu_numbersip
user_token=seu_user_token
oauth_client_id=seu_client_id
oauth_client_secret=seu_client_secret
access_token=
refresh_token=
napikey=
caller=1049
target_number=11999999999
```

## Fluxo de teste recomendado

1. Execute a requisição de OAuth para gerar `access_token`.
2. Salve `access_token` no environment.
3. Teste `GET /balance`.
4. Teste `POST /calls/` com `caller` e `called`.
5. Teste OTP ou WhatsApp templates conforme o caso de uso.

## Quando usar Postman

Use Postman para homologação, troubleshooting e demonstrações rápidas. Para produção, use SDKs ou código próprio no backend da aplicação.
