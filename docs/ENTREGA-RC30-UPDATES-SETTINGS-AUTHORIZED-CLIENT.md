# SAC Ecossistema Gabo v1.0.2-rc30 - Atualizador online nas configurações e cliente autorizado

Data: 2026-07-08

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc30-updates-settings-authorized-client-online-update.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc30-updates-settings-authorized-client-cpanel.zip
gabo-updates-v083-gws-v437-sac-rc30-checksums.sha256
```

## SHA-256

```text
813c9a340a53f40a9634de98bbf292b652fb0bd2b13f1fa1576c770630ea4c5b  gabo-sac-ecosistema-gabo-v1.0.2-rc30-updates-settings-authorized-client-online-update.zip
813c9a340a53f40a9634de98bbf292b652fb0bd2b13f1fa1576c770630ea4c5b  gabo-sac-ecosistema-gabo-v1.0.2-rc30-updates-settings-authorized-client-cpanel.zip
```

## Escopo

- Centraliza configuração do Gabo Updates na tela `/updates` e na área de configurações do SAC.
- Adiciona campos `Servidor Gabo Updates`, `Domínio autorizado` e `Token do cliente`.
- Envia `X-Gabo-Client-Domain` e `X-Gabo-Client-Token` nas consultas e downloads.
- Mantém busca, download, validação, aplicação manual, busca automática e aplicação automática opcional.
- Compatibiliza o SAC com o controle de clientes autorizados do Gabo Updates v0.8.3.

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
node --check src/services/updateService.js
node --check src/routes/updateRoutes.js
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc30-updates-settings-authorized-client-online-update.zip
```

Resultado: OK.
