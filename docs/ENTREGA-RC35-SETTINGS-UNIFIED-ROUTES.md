# SAC Ecossistema Gabo v1.0.2-rc35 - Configurações unificadas e rota do conector

Data: 2026-07-09

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc35-settings-unified-routes-online-update.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc35-settings-unified-routes-cpanel.zip
gabo-sac-rc35-settings-unified-routes-checksums.sha256
```

## SHA-256

```text
8831a22e0d2de4a3fc2ae3ad02c71f331a536615a5bf7a135e32d009139e0fd0  gabo-sac-ecosistema-gabo-v1.0.2-rc35-settings-unified-routes-online-update.zip
8831a22e0d2de4a3fc2ae3ad02c71f331a536615a5bf7a135e32d009139e0fd0  gabo-sac-ecosistema-gabo-v1.0.2-rc35-settings-unified-routes-cpanel.zip
```

## Correção

- Aplica o padrão visual do Gabo Web Suite em todas as páginas de configuração do SAC, não apenas na página inicial.
- Restaura a tela `public/settings-connector.html`.
- Reforça navegação para `/settings/connector`.
- Inclui fallback estático em `public/settings/connector/index.html`.
- Inclui fallbacks estáticos para as demais páginas em `public/settings/<area>/index.html`.
- Mantém os atributos usados pelo JavaScript operacional (`data-connector-field`, `data-save-connector`, `data-setting`, `data-upload-chatbot`, etc.).
- Mantém integração com Gabo Updates, chave de ativação, domínio autorizado e token.

## Páginas revisadas

```text
/settings
/settings/connector
/settings/branding
/settings/whatsapp
/settings/chatbot
/settings/business-hours
/settings/diagnostics
/settings/notifications
/settings/operators
/settings/manual-update
/settings/node
/settings/cloudflare
/updates
```

## Preservação

```text
.env
storage/
logs/
node_modules/
storage/whatsapp-auth/
```

## Validação

```bash
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc35-settings-unified-routes-online-update.zip
unzip -l gabo-sac-ecosistema-gabo-v1.0.2-rc35-settings-unified-routes-online-update.zip | grep settings-connector
```

Resultado: OK.
