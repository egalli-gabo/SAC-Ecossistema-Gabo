# Contrato Gabo Web Suite -> SAC Ecossistema Gabo

## Objetivo

Definir o limite correto entre a plataforma principal e o SAC.

O **Gabo Web Suite** administra as configuracoes aprovadas e publica comandos/eventos.
O **SAC Ecossistema Gabo** recebe/importa configuracoes, executa mensagens, opera chatbot, WhatsApp, protocolo, filas e diagnosticos.

## Fluxo correto

```text
1. Gabo Web Suite publica configuracao/bundle no SAC.
2. SAC versiona configuracao localmente.
3. Gabo Web Suite envia comando simples:
   - codigo/hash/template/evento;
   - destino;
   - variaveis/contexto;
   - modulo de origem;
   - referencia interna quando existir.
4. SAC resolve template, aplica variaveis e regras.
5. SAC envia pelo WhatsApp.
6. SAC devolve status, protocolo, rastreio e diagnostico.
```

## O que o SAC deve importar

- identidade visual necessaria para o InBox;
- usuarios/operadores autorizados;
- configuracao WhatsApp;
- configuracao completa do chatbot;
- departamentos, filas, SLA e horarios;
- templates/mensagens da plataforma;
- regras de roteamento;
- permissoes operacionais quando aplicavel.

## O que o Gabo Web Suite deve enviar em runtime

O comando deve ser simples e idempotente:

```json
{
  "event": "platform.message.dispatch",
  "template_code": "boleto_vencido",
  "template_hash": "sha256 opcional da versao esperada",
  "destination": "5587999999999",
  "variables": {
    "nome": "Cliente",
    "referencia": "NF-123",
    "valor": "R$ 100,00"
  },
  "origin": {
    "module": "fiscal",
    "record_id": "123",
    "record_type": "invoice"
  },
  "idempotency_key": "fiscal:invoice:123:boleto_vencido"
}
```

## Acoes ja presentes no conector v6

A ultima versao enviada do conector contem:

- `bootstrap`: exporta usuarios, identidade visual, configuracao WhatsApp, chatbot, departamentos, templates e servicos.
- `search`: busca registros no DataStore por clientes, contabilidades, fornecedores, parceiros, orgaos publicos e contratos.
- `create-protocol`: cria solicitacao/protocolo no Ecossistema Gabo.
- `link-conversation`: recebe vinculo de conversa do SAC.
- `sac-sso.php`: SSO do Ecossistema Gabo para o SAC.
- `send-sac-notification-event.php`: exemplo CLI para enviar evento ao SAC.

## Ajustes obrigatorios ainda pendentes

- Evoluir o conector v6 para incluir publicacao de bundle com versao/hash.
- Padronizar comando de disparo por `template_code` e `template_hash`, evitando envio de texto livre quando o template ja existir no SAC.
- Implementar idempotencia no SAC.
- Implementar retorno de status por evento/mensagem.
- Garantir que o SAC nao replique telas administrativas desnecessarias da plataforma principal.
- Manter no SAC apenas telas operacionais e diagnosticas necessarias ao motor.
