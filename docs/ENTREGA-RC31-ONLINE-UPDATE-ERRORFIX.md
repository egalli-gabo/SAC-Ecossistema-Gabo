# SAC Ecossistema Gabo v1.0.2-rc31 - Correção do atualizador online

Data: 2026-07-08

## Pacotes gerados

```text
gabo-sac-ecosistema-gabo-v1.0.2-rc31-online-update-errorfix.zip
gabo-sac-ecosistema-gabo-v1.0.2-rc31-online-update-errorfix-cpanel.zip
gabo-gws-v438-sac-rc31-checksums.sha256
```

## SHA-256

```text
ea5aaca3c325c7275b4cc8928503f6920c39a10ff853472b97cae2385599e0c0  gabo-sac-ecosistema-gabo-v1.0.2-rc31-online-update-errorfix.zip
ea5aaca3c325c7275b4cc8928503f6920c39a10ff853472b97cae2385599e0c0  gabo-sac-ecosistema-gabo-v1.0.2-rc31-online-update-errorfix-cpanel.zip
```

## Problema corrigido

O SAC RC30 podia retornar `internal error` ao buscar atualização online em ambientes Node sem `fetch` global ou em falhas de resposta do Gabo Updates.

## Correções

- Remove dependência de `fetch` global.
- Usa HTTP/HTTPS nativo para consultar o Gabo Updates.
- Usa HTTP/HTTPS nativo para baixar pacote ZIP.
- Adiciona timeout controlado.
- Adiciona erro controlado para resposta não JSON.
- Adiciona erro controlado para ZIP inválido.
- Rotas `/api/updates/*` retornam JSON com `error`, `message` e `http_status`.
- Mantém domínio autorizado e token do cliente.

## Validação

```bash
node --check src/services/updateService.js
node --check src/routes/updateRoutes.js
unzip -t gabo-sac-ecosistema-gabo-v1.0.2-rc31-online-update-errorfix.zip
```

Resultado: OK.
