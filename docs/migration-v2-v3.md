# Migração da API Nvoip v2 para a v3

As novas integrações usam `https://api.nvoip.com.br/v3` com OAuth. O caminho `/v2` é uma camada temporária de compatibilidade: manter uma chamada funcionando por esse caminho não conclui sua migração.

## 1. Troque a autenticação

Crie um cliente OAuth na tela Desenvolvedor do Painel Nvoip, vinculado à sua conta e com os escopos das operações necessárias. Para um backend, habilite `client_credentials` e guarde `client_id` e `client_secret` no cofre da aplicação.

| Uso anterior | Integração v3 |
| --- | --- |
| `napikey` na URL ou `X-Nvoip-Api-Key` legado | OAuth Bearer com escopos |
| `/v2/oauth/token`, concessão por senha com numbersip e token do usuário | `POST https://api.nvoip.com.br/auth/oauth2/token`, `client_credentials` |
| Token legado HS256 | Access token do OAuth central para a API v3 |
| Autenticação em aplicação pública | Authorization Code com PKCE S256 e consentimento; sem segredo no navegador |

Envie o pedido de token como formulário `application/x-www-form-urlencoded`; codifique caracteres especiais, incluindo os valores de `client_id` e `client_secret`. O servidor central aceita clientes cadastrados com `client_secret_post` ou `client_secret_basic`; use o método habilitado para o seu cliente. Os SDKs revisados usam a URL central de emissão, separada da URL dos recursos.

Não existe `/v3/oauth/token`. O fluxo antigo com `grant_type=password`, token do usuário e napikey continua apenas na compatibilidade. A nova chave com hash, validade e escopos é uma entrega separada (NN-5543); este guia usa OAuth e não afirma que a chave já está disponível.

No recurso, use `Authorization: Bearer <token>`. Respeite `expires_in`: o fluxo `client_credentials` pode não devolver refresh token; obtenha outro access token quando expirar. Refresh só deve ser utilizado quando o fluxo e o cliente o habilitarem.

## 2. Revise o contrato, além da URL

Use o [OpenAPI da v3](https://github.com/Nvoip/nvoip-api-v3/blob/main/docs/openapi/openapi.yaml) como referência. Confira método, payload, escopo, resposta e tratamento de erro de cada operação.

- **Saldo:** comece com `GET /v3/balance`, sem efeitos de envio.
- **SMS:** prefira `/v3/sms/sendTemplate`, com template `ACTIVE` da própria conta. `/v3/sms` de texto livre exige liberação explícita da política da conta; a permissão legada não equivale a essa liberação.
- **OTP:** `POST /v3/otp` recebe `phoneNumber` ou `email` e `methods`, por exemplo `{"phoneNumber":"TELEFONE_DE_TESTE","methods":{"sms":true}}`. A validação `GET /v3/check/otp?code=...&key=...` também exige Bearer na cadeia de segurança.
- **2FA:** `POST /v3/2fa` usa `cellPhone`/`email` e `methods`. `GET /v3/check/2fa?token2fa=...&pin=...` usa Bearer, sem napikey na URL.
- **Templates:** há diferenças de resposta, como `templateId` na compatibilidade de SMS e `id` na v3. Não presuma paridade pelo nome do endpoint.
- **Ligações e torpedos:** revise os campos de resultado e o contrato assíncrono, limites, preço de TTS e eventos de cobrança antes de habilitar envios.
- **Rotas exclusivas da compatibilidade:** endpoints como `GET /endcall`, `GET /pricing/catalog` e `GET /torpedo/voice/{uuid}` podem não existir diretamente no `/v3`. Use somente alternativas presentes no contrato da v3; não renomeie a URL automaticamente.
- **Contas gerenciadas:** a identidade vem do token. `managedAccountId` só é válido com vínculo e escopos autorizados. O identificador público da conta é o Numbersip principal, final `001`; não exporte IDs internos do billing.

HTTP 401 indica falha de autenticação; 403 pode indicar falta de escopo, política ou bloqueio; 429 indica limite na v3. Não faça retries ilimitados nem troque para credencial legada para contornar uma recusa.

## 3. Atualize SDKs e exemplos

Confira a versão publicada de [cada SDK](../README.md). A preparação de código ou um PR não atualiza npm, PyPI, Maven, NuGet, RubyGems, Packagist, PowerShell Gallery, LuaRocks, Go Modules nem Homebrew. As novas versões fazem uma alteração incompatível de autenticação; revise as chamadas de emissão do token e as variáveis de ambiente.

As integrações servidor a servidor usam `NVOIP_OAUTH_CLIENT_ID`, `NVOIP_OAUTH_CLIENT_SECRET`, `NVOIP_ACCESS_TOKEN` e, quando suportado, `NVOIP_OAUTH_TOKEN_URL`. Não configure `NVOIP_USER_TOKEN` ou `NVOIP_NAPIKEY` para autenticar a v3.

O [Web SDK](https://github.com/Nvoip/nvoip-web-sdk) mantém OAuth no backend e usa os endpoints da sua aplicação no navegador. Nunca envie o client secret ou o access token da plataforma ao widget.

No [n8n](https://github.com/Nvoip/nvoip-n8n), a credencial recebe o Bearer emitido pelo OAuth central. Configure a renovação no seu fluxo; o node não emite o token automaticamente.

## 4. Importe o Postman e confira o resultado

Use a [coleção oficial derivada do OpenAPI](https://github.com/Nvoip/nvoip-api-v3/tree/main/docs/postman) e seu environment local. A base dos recursos é a v3, e a autenticação usa `/auth`. Não publique segredos ou destinos reais no workspace público. A geração local da coleção e a publicação no Postman são etapas separadas.

Faça primeiro emissão do token e leitura de saldo em uma conta própria de teste. Depois confira cada recurso que sua integração utiliza, com escopos, payload e resposta reais. Operações que enviam SMS, WhatsApp, e-mail, ligações, compram números ou alteram dados exigem um cenário explicitamente autorizado; deixe-as fora do runner padrão.

## 5. Conclua a troca e acompanhe a compatibilidade

Mantenha um inventário dos consumidores e confirme que as requisições novas vão à v3 com OAuth. O cabeçalho `Link` das respostas da compatibilidade aponta para este guia; `Deprecation` indica a depreciação e `Sunset`, quando configurado, informa a data definida de retirada.

Não deduza uma data de sunset pela idade da API. A definição de prazo e comunicação aos clientes pertencem ao NN-5545. Os consumidores internos, anúncios OAuth do MCP e serviços que continuam no legado são acompanhados no NN-5546.

Para o [MCP](knowledge-base/mcp.md), use `https://mcp.nvoip.com.br/mcp` e o OAuth descoberto pelo cliente, com PKCE e consentimento. Não configure napikey, token do usuário ou Bearer manual no fluxo de conexão do Claude.
