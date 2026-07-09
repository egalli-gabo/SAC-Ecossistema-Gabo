# SAC Ecossistema Gabo v1.0.2-rc33 - Atualizador online e UI unificada

Data: 2026-07-09

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc33-update-apply-settings-ui-online-update.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc33-update-apply-settings-ui-cpanel.zip
gabo-gws-v441-sac-rc33-checksums.sha256
```

## SHA-256

```text
ec984ac1d0ece2f4628a556085b5950e4418d88d7b293f4da91a9a2c495735d9  gabo-sac-ecosistema-gabo-v1.0.2-rc33-update-apply-settings-ui-online-update.zip
e14acf7de0710625b20b0f932ff3eed9c2605a7c8c8c855d1ba41a0c4e640478  gabo-sac-ecosistema-gabo-v1.0.2-rc33-update-apply-settings-ui-cpanel.zip
```

## Correção

- Adicionado `src/services/updateApplyService.js`, ausente na RC32, corrigindo falha ao aplicar atualização online.
- Tela `/settings` redesenhada para seguir o mesmo padrão visual do Gabo Web Suite.
- Mantida ingestão de eventos GWS → SAC.
- Mantido atualizador online com domínio autorizado/token do cliente.

## Observação operacional

Se a RC32 já estiver instalada e o atualizador online estiver quebrando, aplicar a RC33 uma vez via cPanel. Depois disso, o atualizador online do SAC passa a ter o serviço necessário para aplicar pacotes.

## Validação

```bash
node --check src/services/updateApplyService.js
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc33-update-apply-settings-ui-online-update.zip
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc33-update-apply-settings-ui-cpanel.zip
```

Resultado: OK.
