# SAC Ecossistema Gabo v1.0.2-rc36 - Rota do conector e geração de segredos

Data: 2026-07-09

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc36-connector-route-secrets-online-update.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc36-connector-route-secrets-cpanel.zip
gabo-gws-v443-sac-rc36-checksums.sha256
```

## SHA-256

```text
8e396e61a93ffea1db4ba01c0a8ee7329ed32d4d2f6200f84f0ea19519c31e6c
```

## Correções

- Corrige a rota `/settings/connector` no backend Node.
- Reinclui `src/app.js` com `connector` na lista de páginas protegidas.
- Reinclui endpoints:
  - `GET /api/connector/config`
  - `POST /api/connector/config`
  - `POST /api/connector/test`
  - `POST /api/connector/generate-secret`
- Reinclui `src/services/sisgaboConnector.js` com configuração por banco `sac_settings`.
- Adiciona botão `Gerar segredo` na tela do conector.
- Exibe a chave HMAC gerada para copiar ao Gabo Web Suite.
- Mantém visual unificado das configurações.

## Validação

```bash
node --check src/app.js
node --check src/routes/apiRoutes.js
node --check src/services/sisgaboConnector.js
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc36-connector-route-secrets-online-update.zip
```

Resultado: OK.
