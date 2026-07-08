# SAC Ecossistema Gabo

Repositório oficial do módulo **SAC Ecossistema Gabo**.

## Objetivo

O SAC Ecossistema Gabo é o motor operacional separado para atendimento WhatsApp/InBox, chatbot, filas, handoff humano, envio de mensagens e execução dos templates configurados no Ecossistema Gabo.

A plataforma principal **Gabo Web Suite / Ecossistema Gabo** continua sendo a origem administrativa das configurações aprovadas, mas o SAC deve carregar essas configurações para dentro do seu próprio runtime e executá-las de forma independente.

## Regra arquitetural corrigida

A plataforma principal não deve operar diretamente o socket WhatsApp nem depender do SAC como simples tela auxiliar.

O fluxo correto é:

```text
Gabo Web Suite
  -> administra configuracoes aprovadas
  -> publica bundle/configuracao para o SAC
  -> envia comando/evento simples com codigo/hash/template/contexto

SAC Ecossistema Gabo
  -> importa e versiona a configuracao
  -> resolve codigo/hash/template
  -> monta texto final com variaveis
  -> aplica chatbot, fila, SLA, protocolo e contexto
  -> envia pelo WhatsApp
  -> devolve status, protocolo, logs e diagnosticos
```

## Responsabilidades do SAC

- Receber e armazenar a configuracao integral do motor WhatsApp/chatbot/template/SLA vinda do Ecossistema Gabo.
- Executar mensagens por codigo/hash/template.
- Manter sessao WhatsApp/Baileys estavel e com controle de concorrencia.
- Controlar chatbot, protocolo, handoff humano, filas, SLA, anexos, audio e midia.
- Expor diagnosticos operacionais para WhatsApp, chatbot, fila, conector e mensagens.
- Operar a interface InBox/SAC aprovada.

## Responsabilidades do Gabo Web Suite

- Ser a origem administrativa das configuracoes.
- Publicar bundle/configuracao para o SAC.
- Enviar comandos simples de disparo por evento/codigo/hash/template.
- Consultar status, logs, protocolos e diagnosticos pelo conector.

## Limite obrigatorio

O SAC nao deve ser uma copia completa do Gabo Web Suite.
Ele deve ser o motor operacional do atendimento, alimentado pelas configuracoes aprovadas da plataforma principal.

## Artefatos de referencia

- `sisgabo.zip`: copia integral da plataforma principal enviada para auditoria.
- `gabo-sisgabo-sac-connector-v6-cpanel.zip`: ultima versao do conector SisGabo -> SAC.
- RC25 atual do SAC: base temporaria a auditar, nao baseline definitivo.

## Proxima etapa

Auditar a plataforma principal, o conector v6 e o SAC atual para separar:

- o que permanece no Gabo Web Suite;
- o que deve ser transferido/importado para dentro do SAC;
- o que deve virar comando/evento/hash;
- o que precisa ser revertido das RCs anteriores;
- o que precisa ser mantido e estabilizado.
