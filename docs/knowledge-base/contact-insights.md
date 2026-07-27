# Como consultar o melhor horário para contato pela API Nvoip

A API V3 da Nvoip pode analisar o histórico agregado de atendimento e indicar
os períodos com maior probabilidade de uma ligação ser atendida. O recurso é
útil para ordenar ações de vendedores, preparar um atendimento ou sugerir um
horário antes de discar.

O resultado é uma estimativa estatística, não uma garantia de atendimento.

## Antes de começar

Você precisa de:

- um OAuth `client_id` e `client_secret` da Nvoip;
- o escopo `call:query` autorizado;
- um backend seguro para guardar o `client_secret`;
- o telefone ou escopo regional que deseja consultar.

Não coloque o `client_secret` no navegador.

## 1. Obtenha um access token

```sh
curl 'https://api.nvoip.com.br/auth/oauth2/token' \
  --user "$NVOIP_OAUTH_CLIENT_ID:$NVOIP_OAUTH_CLIENT_SECRET" \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data 'grant_type=client_credentials&scope=call%3Aquery'
```

Guarde o campo `access_token` somente pelo período informado em `expires_in`.

## 2. Consulte os insights

```sh
curl --get 'https://api.nvoip.com.br/v3/calls/contact-insights' \
  --header "Authorization: Bearer $NVOIP_ACCESS_TOKEN" \
  --header 'Idempotency-Key: crm-opportunity-12345-v1' \
  --data-urlencode 'destination=5511000000000' \
  --data-urlencode 'timezone=America/Sao_Paulo'
```

Use um telefone sintético em exemplos públicos. Não copie telefones reais para
tickets ou logs.

O campo `summary` traz uma leitura rápida. Os campos `bestPeriod`, `topDays`,
`topHours`, `confidence` e `callNow` permitem montar uma experiência mais
detalhada.

Quando `hasData=false`, ainda não existe histórico suficiente para aquela
consulta.

## Idempotência e retries

Envie uma `Idempotency-Key` estável para a operação. Se a resposta se perder e
você precisar repetir exatamente a mesma consulta, reutilize a chave com os
mesmos parâmetros: o retry não consome uma segunda unidade da franquia mensal.
Usar a mesma chave com parâmetros diferentes gera um novo consumo.

Para retries totalmente reproduzíveis, informe também `referenceUtc`.

## Franquia por usuário

Cada usuário possui uma franquia mensal de consultas:

| Plano | Consultas incluídas |
| --- | ---: |
| Free | 100 |
| Startup | 250 |
| Basic | 500 |
| PRO | 1.000 |

O objeto `usage` e os headers `X-RateLimit-Limit` e
`X-RateLimit-Remaining` mostram o consumo atual. Quando a franquia termina, as
consultas excedentes podem continuar. O tempo de processamento é arredondado
para cima, com mínimo de um minuto faturável por consulta excedente, ao preço
inicial de R$ 0,02 por minuto.

Exemplo:

```json
{
  "usage": {
    "feature": "contact_insights",
    "plan": "Startup",
    "periodStart": "2026-07-01",
    "periodEnd": "2026-08-01",
    "included": 250,
    "used": 127,
    "remaining": 123,
    "overage": 0,
    "overageThisRequest": false,
    "overageBillingUnit": "MINUTE",
    "billableMinutesThisRequest": 1,
    "overageBillableMinutes": 0,
    "billingStatus": "INCLUDED"
  }
}
```

Em consultas excedentes, a resposta também apresenta `overageUnitPriceBrl`,
`billableMinutesThisRequest` e `billableAmountBrl`. Consulte sempre o preço
comercial publicado antes de habilitar chamadas automáticas em grande volume.

## Boas práticas de integração

- Faça a consulta quando o usuário abrir a ação de ligação, não ao carregar uma
  lista inteira de contatos.
- Não inicie uma ligação automaticamente apenas porque `callNow` recomenda o
  momento atual.
- Use o fuso real da operação ou do contato.
- Trate `503` e `504` com uma mensagem amigável e permita que o fluxo manual
  continue quando isso for seguro.
- Monitore a franquia pelos headers e avise antes de iniciar consumo excedente.

## Erros comuns

- `400`: telefone, fuso, referência ou chave de idempotência inválidos;
- `401`: access token ausente, inválido ou expirado;
- `403`: o client não possui `call:query` ou o perfil não é elegível;
- `429`: limite rígido configurado para o recurso;
- `503`: cálculo ou medição temporariamente indisponível;
- `504`: tempo limite excedido.

Perfis de clientes de revendedores não têm acesso a este recurso.
