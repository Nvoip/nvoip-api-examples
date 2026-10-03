# Release flow dos SDKs Nvoip

Este fluxo padroniza publicação dos SDKs nos gerenciadores de pacotes.

## Regra geral

1. Alterar código e README.
2. Atualizar versão do pacote.
3. Rodar validação local.
4. Fazer commit e push.
5. Criar tag `vX.Y.Z`.
6. Criar GitHub Release a partir da tag.
7. Deixar o workflow `Publish package` publicar no registry.
8. Conferir indexação pública no registry.

## Versionamento

Use SemVer:

- `PATCH` para correção, docs publicadas junto do pacote ou ajuste de exemplo.
- `MINOR` para novos endpoints ou novas funções.
- `MAJOR` para quebra de API pública do SDK.

## Pacotes e registries

| Repositório | Registry | Pacote |
| --- | --- | --- |
| `nvoip-node` | npm | `nvoip-node` |
| `nvoip-web-sdk` | npm | `nvoip-web-sdk` |
| `nvoip-python` | PyPI | `nvoip` |
| `nvoip-php` | Packagist | `nvoip/nvoip-php` |
| `nvoip-go` | Go Modules | `github.com/Nvoip/nvoip-go/v3` |
| `nvoip-java` | Maven Central | `br.com.nvoip:nvoip-java` |
| `nvoip-dotnet` | NuGet | `Nvoip` |
| `nvoip-ruby` | RubyGems | `nvoip` |
| `nvoip-powershell` | PowerShell Gallery | `Nvoip` |
| `nvoip-lua` | LuaRocks | `nvoip` |
| `nvoip-shell` | Homebrew | `Nvoip/tap/nvoip-shell` |

## Segredos

Segredos devem ficar em GitHub Actions Secrets do repositório ou em trusted publishing quando o registry suportar.

Nunca commitar `napikey`, `user-token`, `client_secret`, token de package manager ou `Basic Auth` pré-gerado.
