# SAC Ecossistema Gabo v1.0.2-rc34 - Ativação Gabo Updates

Data: 2026-07-09

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc34-activation-update-auth-online-update.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc34-activation-update-auth-cpanel.zip
gabo-updates-v084-gws-v442-sac-rc34-checksums.sha256
```

## SHA-256

```text
d4cacff4f22ac3918c16575287cacf236db5d64fd7a95a1c5be52f84c3dbef25  gabo-sac-ecosistema-gabo-v1.0.2-rc34-activation-update-auth-online-update.zip
d4cacff4f22ac3918c16575287cacf236db5d64fd7a95a1c5be52f84c3dbef25  gabo-sac-ecosistema-gabo-v1.0.2-rc34-activation-update-auth-cpanel.zip
```

## Escopo

- Adiciona verificação de chave de ativação gerada pelo Gabo Updates.
- Salva a chave como token do atualizador online do SAC.
- Mantém domínio autorizado e `X-Gabo-Client-Token` nas consultas/downloads.
- Inclui tela/atalho de ativação na área de configurações/updates.
- Adiciona rotas:
  - `GET /api/updates/activation`
  - `POST /api/updates/activation`

## Fluxo

```text
Gabo Updates
  -> gera chave de ativação vinculada a CPF/CNPJ e domínio
SAC
  -> recebe somente a chave
  -> valida em /api/activation/verify
  -> salva a chave como token do atualizador online
  -> passa a consultar e baixar pacotes com X-Gabo-Client-Domain e X-Gabo-Client-Token
```

## Validação

```bash
node --check src/services/updateService.js
node --check src/routes/updateRoutes.js
node --check src/services/updateApplyService.js
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc34-activation-update-auth-online-update.zip
```

Resultado: OK.
