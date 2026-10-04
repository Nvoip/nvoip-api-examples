# Status dos pacotes públicos da API v3

Situação verificada em 3 de outubro de 2026. As versões abaixo contêm a migração para a v3 e OAuth; uma versão anterior disponível no registry não comprova a publicação desta entrega.

| SDK | Registry | Versão v3 | Publicação |
| --- | --- | --- | --- |
| Node.js | npm `nvoip-node` | 3.0.0 | Publicado; instalação do npm e OAuth/saldo conferidos |
| Web SDK | npm `nvoip-web-sdk` | 1.0.0 | Pendente: acesso de publicação OIDC ainda não confirmado |
| Python | PyPI `nvoip` | 3.0.1 | Publicado |
| PHP | Packagist `nvoip/nvoip-php` | 3.0.0 | Publicado |
| Go | Go Modules `github.com/Nvoip/nvoip-go/v3` | 3.0.0 | Publicado |
| Java | Maven Central `br.com.nvoip:nvoip-java` | 1.0.0 | Publicado; consumidor do JAR público e OAuth/saldo conferidos |
| .NET | NuGet `Nvoip` | 1.0.1 | Publicado; substitui 1.0.0 por correção do ciclo de vida HTTP |
| Ruby | RubyGems `nvoip` | 3.0.1 | Publicado |
| PowerShell | PowerShell Gallery `Nvoip` | 1.0.0 | Publicado |
| Lua | LuaRocks `nvoip` | 1.0.1-1 | Publicado; instalação do registry e OAuth/saldo conferidos |
| Shell/Linux | Homebrew tap `Nvoip/tap/nvoip-shell` | 1.0.0 | Publicado |

Para Web, use o código revisado e a tag da versão no repositório ou aguarde a disponibilização no registry. Não instale uma versão anterior esperando o comportamento novo.

Publicação e teste funcional são estados separados. Os exemplos de instalação em cada guia fixam a versão desta migração. Nenhuma integração servidor a servidor deve guardar `client_secret` no navegador.
