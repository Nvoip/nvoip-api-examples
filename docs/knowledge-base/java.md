# Como integrar a API Nvoip com Java

Repositório: https://github.com/Nvoip/nvoip-java

Pacote Maven: `br.com.nvoip:nvoip-java`

## Instalação Maven

```xml
<dependency>
  <groupId>br.com.nvoip</groupId>
  <artifactId>nvoip-java</artifactId>
  <version>1.0.0</version>
</dependency>
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
mvn test
mvn -q exec:java
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.

## Disponibilidade da versão v3

A publicação desta versão no registry ainda depende da regularização das credenciais de publicação. Enquanto ela não estiver disponível, use o código revisado do repositório ou aguarde a publicação; uma versão antiga do pacote não oferece o caminho v3/OAuth descrito aqui.
