# Plano RC26 - Reconstrucao controlada

## Regra principal

Nao gerar nova RC apenas empilhando patches.
A RC26 deve nascer de auditoria entre tres bases:

1. plataforma principal `sisgabo.zip`;
2. conector `gabo-sisgabo-sac-connector-v6-cpanel.zip`;
3. SAC atual RC25.

## Objetivo da RC26

Entregar o **SAC Ecossistema Gabo** como motor operacional correto:

- configurações importadas do Ecossistema Gabo para dentro do SAC;
- execução por código/hash/template/evento;
- WhatsApp estável com processo único;
- chatbot funcionando com protocolo e atendimento entrando;
- operador assumindo atendimento de forma persistente;
- plataforma principal enviando comandos simples;
- diagnosticos objetivos para conector, bot, fila, WhatsApp e mensagens.

## Fase 1 - Auditoria obrigatoria

- Mapear telas e arquivos da plataforma principal relacionados a WhatsApp, chatbot, mensagens da plataforma, atualizador e conector.
- Mapear exatamente o contrato do conector v6.
- Mapear o que a RC25 duplicou indevidamente.
- Mapear quais correcoes das RC17-RC25 devem ser mantidas.
- Mapear quais correcoes devem ser revertidas.

## Fase 2 - Alteracoes no Gabo Web Suite

- Manter a plataforma principal como origem administrativa.
- Garantir exportacao/publicacao do bundle de configuracao para o SAC.
- Garantir envio de comandos simples por evento/codigo/hash/template.
- Garantir consulta de status/logs/diagnosticos pelo conector.

## Fase 3 - Alteracoes no conector

- Evoluir `sac-connector.php` para action de publicacao de bundle com versao/hash.
- Evoluir envio de eventos para usar `template_code`, `template_hash`, `variables` e `idempotency_key`.
- Manter SSO e busca de registros.
- Garantir assinatura HMAC em todos os comandos.

## Fase 4 - Alteracoes no SAC

- Importar e persistir bundles do Ecossistema Gabo.
- Resolver mensagens por template local do SAC.
- Tratar comando/evento de envio como idempotente.
- Manter motor WhatsApp com lock de processo unico.
- Corrigir pipeline minimo:
  - inbound recebido;
  - chatbot responde;
  - protocolo gerado;
  - atendimento entra na lista;
  - operador assume;
  - mensagem assume enviada;
  - envio manual funciona;
  - encerramento vai para avaliacao;
  - status retorna ao Gabo Web Suite.

## Fase 5 - Validacao minima antes de pacote

Nenhum pacote RC26 deve ser entregue sem validar:

- `npm run check`;
- integridade ZIP;
- diagnostico local de rotas principais;
- existencia de migrations esperadas;
- existencia do contrato de conector;
- ausencia de `.env`, secrets, sessoes, storage, logs e node_modules;
- teste logico do fluxo de comando por template.
