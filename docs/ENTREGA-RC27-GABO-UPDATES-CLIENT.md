# SAC Ecossistema Gabo v1.0.2-rc27 - Cliente Gabo Updates

Data: 2026-07-08

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc27-gabo-updates-client-online-update.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc27-gabo-updates-client-cpanel.zip
gabo-sac-rc27-gabo-updates-checksums.sha256
```

## SHA-256

```text
f9a70ad7e68cf04e57e197c1e468dcc1cc73e5951e5997d8c04989b77a3681fa  gabo-sac-ecosistema-gabo-v1.0.2-rc27-gabo-updates-client-online-update.zip
f9a70ad7e68cf04e57e197c1e468dcc1cc73e5951e5997d8c04989b77a3681fa  gabo-sac-ecosistema-gabo-v1.0.2-rc27-gabo-updates-client-cpanel.zip
```

## Escopo

Conecta o SAC Ecossistema Gabo ao Gabo Updates como cliente oficial de atualização.

Produto oficial:

```text
sac_ecossistema_gabo
```

Canais oficiais:

```text
alpha   -> Alpha / RC
beta    -> Beta / Homologação
release -> Lançamento Final
```

## Alterações

- Atualiza `src/services/updateService.js` para consultar o Gabo Updates v0.8.x.
- Atualiza `src/routes/updateRoutes.js` com:
  - `/api/updates/config`
  - `/api/updates/check`
  - `/api/updates/versions`
  - `/api/updates/stage-latest`
- Atualiza `/updates` com seleção de canal Alpha, Beta e Release.
- Permite baixar e validar pacote publicado no Gabo Updates.
- Registra pacote online em `sac_manual_update_jobs`.
- Usa o motor manual existente para aplicar o pacote com backup e preservação.
- Valida assinatura ZIP e SHA-256 antes de permitir aplicação.

## Endpoints usados

```text
GET /api/latest?product=sac_ecossistema_gabo&channel=beta
GET /api/versions?product=sac_ecossistema_gabo&channel=beta
```

## Compatibilidade

Canais antigos são normalizados:

```text
sac-homologacao -> beta
homologacao     -> beta
rc              -> alpha
producao        -> release
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
npm run check
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc27-gabo-updates-client-online-update.zip
```

Resultado: OK.
