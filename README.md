# Nvoip API Examples

Índice oficial da [Nvoip](https://www.nvoip.com.br/) com SDKs, exemplos e kits públicos para integrar a API v2.

O objetivo deste repositório é facilitar a descoberta do material certo por linguagem, stack e caso de uso, sem obrigar quem usa uma tecnologia específica a baixar um pacote grande com exemplos irrelevantes.

## Fluxos principais

Os kits abaixo priorizam os fluxos mais usados da API:

- OAuth e geração de `access_token`
- disparo de chamadas
- OTP e validação de código
- envio de templates de WhatsApp
- envio de SMS
- consulta de saldo

## Escolha rápida

Se você quer um fluxo embutível de telefone + código para web:

- [nvoip-web-sdk](https://github.com/Nvoip/nvoip-web-sdk)

Se você quer testar a API sem SDK:

- [nvoip-curl-examples](https://github.com/Nvoip/nvoip-curl-examples)
- [Postman Workspace da Nvoip](https://nvoip-api.postman.co/workspace/e671d01f-168a-4c38-8d0e-c217229dd61a/team-quickstart)

Se você quer integrar pelo backend da sua aplicação:

- [nvoip-node](https://github.com/Nvoip/nvoip-node)
- [nvoip-python](https://github.com/Nvoip/nvoip-python)
- [nvoip-php](https://github.com/Nvoip/nvoip-php)
- [nvoip-go](https://github.com/Nvoip/nvoip-go)
- [nvoip-java](https://github.com/Nvoip/nvoip-java)
- [nvoip-dotnet](https://github.com/Nvoip/nvoip-dotnet)
- [nvoip-ruby](https://github.com/Nvoip/nvoip-ruby)
- [nvoip-powershell](https://github.com/Nvoip/nvoip-powershell)
- [nvoip-lua](https://github.com/Nvoip/nvoip-lua)
- [nvoip-shell](https://github.com/Nvoip/nvoip-shell)

Se você quer automação e operação:

- [nvoip-n8n](https://github.com/Nvoip/nvoip-n8n)
- [nvoip-zabbix](https://github.com/Nvoip/nvoip-zabbix)

## Repositórios públicos

| Repositório | Stack | Uso principal |
| --- | --- | --- |
| [nvoip-web-sdk](https://github.com/Nvoip/nvoip-web-sdk) | Browser / JavaScript | Widget embutível para autenticação com telefone + código |
| [nvoip-curl-examples](https://github.com/Nvoip/nvoip-curl-examples) | cURL | Requisições prontas para teste rápido e troubleshooting |
| [nvoip-node](https://github.com/Nvoip/nvoip-node) | Node.js | SDK e exemplos server-side |
| [nvoip-python](https://github.com/Nvoip/nvoip-python) | Python | SDK e exemplos server-side |
| [nvoip-php](https://github.com/Nvoip/nvoip-php) | PHP | SDK e exemplos server-side |
| [nvoip-go](https://github.com/Nvoip/nvoip-go) | Go | SDK e exemplos server-side |
| [nvoip-java](https://github.com/Nvoip/nvoip-java) | Java | SDK e exemplos server-side |
| [nvoip-dotnet](https://github.com/Nvoip/nvoip-dotnet) | .NET | SDK e exemplos server-side |
| [nvoip-ruby](https://github.com/Nvoip/nvoip-ruby) | Ruby | SDK e exemplos server-side |
| [nvoip-powershell](https://github.com/Nvoip/nvoip-powershell) | PowerShell | Scripts e automações administrativas |
| [nvoip-lua](https://github.com/Nvoip/nvoip-lua) | Lua | SDK e exemplos leves para integrações específicas |
| [nvoip-shell](https://github.com/Nvoip/nvoip-shell) | Shell / Linux | Scripts prontos para servidores Linux |
| [nvoip-zabbix](https://github.com/Nvoip/nvoip-zabbix) | Zabbix | Alertas via SMS e voz usando a API v2 |
| [nvoip-n8n](https://github.com/Nvoip/nvoip-n8n) | n8n | Nós e fluxos para automação low-code |

## Credenciais usadas nos exemplos

A maioria dos kits usa o mesmo conjunto de variáveis de ambiente:

- `NVOIP_NUMBERSIP`
- `NVOIP_USER_TOKEN`
- `NVOIP_OAUTH_CLIENT_ID`
- `NVOIP_OAUTH_CLIENT_SECRET`
- `NVOIP_ACCESS_TOKEN`

Quando o fluxo exigir autenticação OAuth, a preferência atual é sempre por `client_id` + `client_secret`.

## Documentação oficial

- [Apiary da Nvoip API](https://nvoip.docs.apiary.io/)
- [Página da API no site da Nvoip](https://www.nvoip.com.br/api/)

## Observações

- Os exemplos usam valores ilustrativos e devem ser adaptados com as credenciais reais da conta.
- Este repositório é um índice. O código executável fica separado por linguagem para melhorar busca, indexação e manutenção.
