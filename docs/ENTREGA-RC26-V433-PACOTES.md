# Entrega em três pacotes - Gabo Web Suite v433 / Conector v7 / SAC RC26

Data: 2026-07-08

## Pacotes gerados

```text
gabo-web-suite-v12-rc-v433-sac-connector-template-dispatch-cpanel.zip
gabo-web-suite-v12-rc-v433-manual-update.zip
gabo-sisgabo-sac-connector-v7-template-dispatch-cpanel.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc26-template-dispatch-cpanel.zip
gabo-sac-rc26-manual-frontend-update.zip
gabo-ecosistema-sac-rc26-v433-checksums.sha256
```

## SHA-256

```text
dfa4bfde5413270795a9392f7ad9f864b4d904ba1fe0c0ce45c8f5447291999f  gabo-web-suite-v12-rc-v433-sac-connector-template-dispatch-cpanel.zip
dfa4bfde5413270795a9392f7ad9f864b4d904ba1fe0c0ce45c8f5447291999f  gabo-web-suite-v12-rc-v433-manual-update.zip
bbf419b8b0b75761cef15e65b4734c4e8f0987721f783cc1f82f6edc28b729a6  gabo-sisgabo-sac-connector-v7-template-dispatch-cpanel.zip
6eeb30dac794e7ed421f72b5a22982341e0aa312e6c3ece1684af20011051513  gabo-sac-ecosistema-gabo-v1.0.2-rc26-template-dispatch-cpanel.zip
6eeb30dac794e7ed421f72b5a22982341e0aa312e6c3ece1684af20011051513  gabo-sac-rc26-manual-frontend-update.zip
```

## Pacote 1 - Gabo Web Suite v12-rc-v433

- Reabilita atualização manual por upload ZIP na tela de atualizações.
- Mantém servidor de updates como opcional, não obrigatório.
- Remove a opção de upload JSON para configurar chatbot no Gabo Web Suite.
- Mantém `/configuracoes/chatbot` apenas para mensagens sistêmicas da plataforma.
- Mapeia mensagens da plataforma por `template_code` e `template_hash`.
- Encaminha eventos de WhatsApp da plataforma para o SAC por HMAC.
- Inclui conector v7.

## Pacote 2 - Conector SisGabo/SAC v7

- Mantém `bootstrap`.
- Adiciona `config-bundle` / `bootstrap-bundle`.
- Adiciona `platform-message-map`.
- Adiciona `dispatch-preview`.
- CLI de evento passa a trabalhar com `template_code`, `variables` e `idempotency_key`.

## Pacote 3 - SAC Ecossistema Gabo RC26

- Recebe bundle do Gabo Web Suite em `/internal/sync/config-bundle`.
- Importa templates da plataforma para `sac_message_templates`.
- Recebe acionadores em `/internal/events/notification`.
- Resolve `template_code` localmente no SAC.
- Renderiza com `variables`.
- Enfileira para envio WhatsApp.
- Mantém chatbot v393 com `engine.enabled=true` em runtime.
- Mantém regra de apresentação automática do operador no handoff.

## Validações executadas

```bash
cd /mnt/data/sac_rc26_work && npm run check
node --check /mnt/data/sac_rc26_work/src/routes/internalRoutes.js
unzip -t gabo-web-suite-v12-rc-v433-sac-connector-template-dispatch-cpanel.zip
unzip -t gabo-sisgabo-sac-connector-v7-template-dispatch-cpanel.zip
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc26-template-dispatch-cpanel.zip
```

Resultado: OK.

## Observação

A validação foi local/sintática e de integridade ZIP. Não foram incluídos `.env`, secrets, sessões WhatsApp, `storage`, `logs` nem `node_modules` nos pacotes do SAC. O pacote Gabo Web Suite preserva arquivos de exemplo quando existentes, mas exclui `.env` reais e storage.