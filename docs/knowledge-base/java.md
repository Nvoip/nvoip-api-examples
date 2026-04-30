# Como integrar a API Nvoip com Java

Repositório: https://github.com/Nvoip/nvoip-java

Pacote Maven: `br.com.nvoip:nvoip-java`

## Instalação Maven

```xml
<dependency>
  <groupId>br.com.nvoip</groupId>
  <artifactId>nvoip-java</artifactId>
  <version>0.1.0</version>
</dependency>
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
mvn test
mvn -q exec:java
```

## Recursos cobertos

OAuth, chamadas, OTP, WhatsApp templates, SMS e saldo.
