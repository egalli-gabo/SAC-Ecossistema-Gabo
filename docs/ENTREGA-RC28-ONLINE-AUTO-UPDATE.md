# SAC Ecossistema Gabo v1.0.2-rc28 - Atualizador online automático

Data: 2026-07-08

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc28-online-auto-update.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc28-online-auto-cpanel.zip
gabo-sac-rc28-online-auto-checksums.sha256
```

## SHA-256

```text
5d6e9c9c238a7319284bbcc695ed40de81da2eeb37d9fb9f99c2aae995ddebf6  gabo-sac-ecosistema-gabo-v1.0.2-rc28-online-auto-update.zip
5d6e9c9c238a7319284bbcc695ed40de81da2eeb37d9fb9f99c2aae995ddebf6  gabo-sac-ecosistema-gabo-v1.0.2-rc28-online-auto-cpanel.zip
```

## Escopo

Inclui no SAC um atualizador online semelhante ao do Gabo Web Suite, usando o Gabo Updates como servidor oficial.

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

## Funcionalidades incluídas

- Botão `Buscar atualização`.
- Botão `Baixar e validar`.
- Botão `Buscar e aplicar agora`.
- Configuração de automação na tela `/updates`.
- Busca automática em intervalo configurável.
- Download e validação automática opcional.
- Aplicação automática opcional com backup.
- Janela de manutenção opcional.
- Histórico de execuções automáticas.
- Preservação do motor manual já existente para aplicar pacotes.

## Novas rotas

```text
GET  /api/updates/auto-config
POST /api/updates/auto-config
POST /api/updates/auto-run-now
POST /api/updates/apply-latest
```

## Nova migração

```text
migrations/022_rc28_online_auto_update.sql
```

Cria a tabela:

```text
sac_update_auto_runs
```

E adiciona a configuração inicial em `sac_settings`.

## Segurança operacional

A busca automática fica habilitada por padrão, mas a aplicação automática fica desabilitada por padrão. O superadministrador pode habilitar aplicação automática e janela de manutenção pela tela `/updates`.

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
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc28-online-auto-update.zip
```

Resultado: OK.
