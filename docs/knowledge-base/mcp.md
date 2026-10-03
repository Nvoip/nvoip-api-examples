# Como conectar o MCP da Nvoip

Use a URL `https://mcp.nvoip.com.br/mcp` no cliente MCP. A autenticação usa o servidor OAuth compartilhado `https://api.nvoip.com.br/auth`, com authorize/token em `/auth/oauth2/*`, PKCE e consentimento do usuário.

## Claude e Claude Desktop

Adicione a URL do MCP e mantenha Client ID e Client Secret vazios. Depois de adicionar, clique em conectar para abrir o OAuth. A descoberta inicial pode receber 401 sem token: o cliente deve abrir a autenticação antes de consultar ferramentas.

## Claude Code

```sh
claude mcp add --transport http --scope user nvoip https://mcp.nvoip.com.br/mcp
```

Abra `/mcp` e conclua a autenticação. Não configure `napikey`, token do usuário nem Bearer manual nesse fluxo.

## Outras integrações

O MCP e a API pública têm audiências e escopos próprios: não reutilize um token do MCP como se fosse um token genérico da API. Para integração servidor a servidor com a API v3, consulte [Primeiros passos](getting-started.md).

Aliases de descoberta legados podem continuar anunciados durante a compatibilidade; isso não transforma `/v2` em base das novas integrações. A migração dos consumidores internos e desses anúncios é acompanhada no NN-5546.
