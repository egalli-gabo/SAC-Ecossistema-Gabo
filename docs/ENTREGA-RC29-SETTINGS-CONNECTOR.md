# SAC Ecossistema Gabo v1.0.2-rc29 - Configurações e conector integrado

Data: 2026-07-08

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc29-settings-connector-online-update.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc29-settings-connector-cpanel.zip
gabo-settings-connector-rc29-v436-checksums.sha256
```

## SHA-256

```text
d499e6f3ebfda3a003b681f6acc8b2d6af8b4e19bd8d5eecce2ff92532a5fad4  gabo-sac-ecosistema-gabo-v1.0.2-rc29-settings-connector-online-update.zip
d499e6f3ebfda3a003b681f6acc8b2d6af8b4e19bd8d5eecce2ff92532a5fad4  gabo-sac-ecosistema-gabo-v1.0.2-rc29-settings-connector-cpanel.zip
```

## Escopo

- Redesenha a página inicial de configurações do SAC.
- Inclui nova página `/settings/connector`.
- Permite configurar o conector Gabo Web Suite pela interface.
- Salva URL, integration ID, segredo HMAC e ações no banco `sac_settings`.
- Mantém `.env` como fallback, mas não exige mais edição via cPanel para trocar dados do conector.
- Adiciona teste controlado do conector sem erro 500.

## Arquivos principais alterados

```text
public/settings.html
public/settings-connector.html
public/assets/sac-settings-rc29.css
public/assets/sac-admin-settings.js
src/app.js
src/routes/apiRoutes.js
src/services/ecosystemClient.js
src/services/sisgaboConnector.js
migrations/023_rc29_settings_connector.sql
```

## Novos endpoints

```text
GET  /api/connector/config
POST /api/connector/config
POST /api/connector/test
```

## Preservação

```text
.env
storage/
logs/
node_modules/
storage/whatsapp-auth/
```

## Regra mantida

O prompt JSON do chatbot continua aceito para upgrade/importação somente no SAC.

## Validações

```bash
node --check src/app.js
node --check src/routes/apiRoutes.js
node --check src/services/ecosystemClient.js
node --check src/services/sisgaboConnector.js
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc29-settings-connector-online-update.zip
```

Resultado: OK.
