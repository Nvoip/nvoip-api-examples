# Como integrar alertas do Zabbix com a Nvoip

Repositório: https://github.com/Nvoip/nvoip-zabbix

Use este kit para enviar alertas do Zabbix por SMS ou torpedo de voz usando a API v2 da Nvoip.

## Configuração no servidor

Defina as variáveis no ambiente do serviço Zabbix:

```bash
export NVOIP_NUMBERSIP="seu_numbersip"
export NVOIP_USER_TOKEN="seu_user_token"
export NVOIP_OAUTH_CLIENT_ID="seu_client_id"
export NVOIP_OAUTH_CLIENT_SECRET="seu_client_secret"
export NVOIP_CALLER="1049"
```

## Instalação dos scripts

```bash
sudo cp Scripts/*.sh /usr/lib/zabbix/alertscripts/
sudo chown zabbix:zabbix /usr/lib/zabbix/alertscripts/*.sh
sudo chmod 750 /usr/lib/zabbix/alertscripts/*.sh
```

## Validar configuração

```bash
/usr/lib/zabbix/alertscripts/check_nvoip_zabbix_config.sh
```

## Media Types

Configure `send_sms_nvoip_zabbix.sh` para SMS e `send_torpedovoz_nvoip_zabbix.sh` para voz.

Use os parâmetros descritos em `templates/media-types.md` no repositório.
