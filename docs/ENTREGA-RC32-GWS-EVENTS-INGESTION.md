# SAC Ecossistema Gabo v1.0.2-rc32 - Recepção de eventos do Gabo Web Suite

Data: 2026-07-09

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc32-gws-events-ingestion-online-update.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc32-gws-events-ingestion-cpanel.zip
gabo-gws-v439-sac-rc32-checksums.sha256
```

## SHA-256

```text
d18bc5bcf7bd84195038b992426283e0bb8c55dd152c55c16114dbf6b7f8b0c2
```

## Escopo

- O SAC passa a receber eventos assinados do Gabo Web Suite em `/internal/events/notification`.
- Eventos `platform.template.updated` sincronizam templates locais em `sac_message_templates`.
- Eventos `platform.templates.bundle.updated` sincronizam bundles de templates.
- Eventos com destino/destination/phone/to renderizam template e entram em `sac_message_queue`.
- Cria registro em `sac_external_events` com idempotência por `idempotency_key`.
- Cria registro em `sac_whatsapp_events` e auditoria em `sac_audit_logs`.

## Nova migração

```text
migrations/024_rc32_gws_event_ingestion.sql
```

Cria:

```text
sac_external_events
```

## Arquivos principais

```text
src/routes/internalRoutes.js
src/services/gwsEventIngestion.js
migrations/024_rc32_gws_event_ingestion.sql
public/settings.html
```

## Fluxo

```text
GWS salva template/mensagem sistêmica
  -> GWS assina evento via conector
  -> SAC recebe evento
  -> SAC sincroniza template
  -> se houver destino, renderiza mensagem
  -> SAC enfileira para envio pelo WhatsApp
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
node --check src/routes/internalRoutes.js
node --check src/services/gwsEventIngestion.js
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc32-gws-events-ingestion-online-update.zip
```

Resultado: OK.
