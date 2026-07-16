# SAEG 2.0.0-rc.9 — Eco e contenção da tempestade de mensagens

Data: 2026-07-16  
Base do pacote: SAEG `2.0.0-rc.8`  
Dependências de homologação: GWS `v12-rc-v491`, GUP `1.0.1`, MariaDB 10.6+, Node 20+

## Incidente bloqueador

O primeiro `Oi` foi interpretado como nome e a árvore avançou/disparou mensagens em sequência, repetindo protocolo e opções até causar restrição temporária do WhatsApp pela Meta. O canal foi desconectado para conter o incidente.

## Correções registradas

- Uma entrada avança no máximo um estado; a Eco aguarda resposta válida antes da próxima pergunta.
- Saudações como `Oi`, `Bom dia`, `Boa tarde` e `Boa noite` não são aceitas como nome.
- Protocolo único de 17 dígitos, telefone detectado confirmado/corrigido e `reply_jid` preservado como destino real.
- LGPD com aceite explícito; recusa encerra e audita `CLIENTE_RECUSOU_LGPD`.
- Encerramento voluntário com confirmação antes do handoff.
- Segmentos e assuntos próprios para Certificados Digitais, Gabo Sistemas, Gabo Studio Web, Gabo Assistance, Gabo Prime e Setor Público.
- Setor Público por CNPJ do órgão, razão social vinda do GWS e CPF apenas quando o atendimento for pessoal.
- Consulta HMAC ao GWS para CPF/CNPJ, vínculos e atendimentos em andamento.
- Handoff idempotente, apresentação automática do colaborador e resumo interno completo para usuários autorizados.
- Pesquisa em dois passos: problema solucionado e nota de 1 a 5, reutilizando a escala do card Qualidade do Atendimento do GWS.
- `Enter` envia e `Shift+Enter` quebra linha; botão telefônico usa o número confirmado.
- Outbox idempotente e serializada por conversa, pequeno atraso de digitação, presença `composing` e eventos sem ID do provedor em quarentena.
- `tools/message-buffer.js`: inspeção por padrão, pausa global, quarentena auditável e retomada explícita; não apaga histórico.
- Nenhuma alteração visual no GWS ou no GUP.

## Pacote

`gabo-saeg-v2.0.0-rc.9-eco-message-safety-full.zip`

SHA-256:

```text
f56119d962527e7aa6ee86c0e90b3cbacc2ca8eb011c1fed8482601a7f7eb9c2
```

## Validação local

- 40/40 testes Node aprovados.
- 146/146 verificações de release aprovadas.
- 122 arquivos conferidos por SHA-256.
- ZIP íntegro.
- Segredos transitórios, `.env`, `node_modules` e dados operacionais não foram incorporados.

## Ordem segura de homologação

1. Manter o WhatsApp desconectado.
2. Criar backup do GWS v490, SAEG rc.8, banco e storage.
3. Aplicar GWS v491 e confirmar `POST /api/saeg/lookup` com HMAC real.
4. Aplicar SAEG rc.9, instalar dependências e executar migrations, inclusive `007_eco_conversation_safety.sql`.
5. Executar `npm run buffer:inspect`.
6. Revisar o relatório e, se correto, executar `node tools/message-buffer.js --apply --confirm=QUARANTINE`.
7. Validar filas, consulta GWS, protocolo único, escala 1–5 e outbox sem pendências inesperadas.
8. Executar `node tools/message-buffer.js --resume --confirm=RESUME`, ainda desconectado.
9. Reconectar e fazer um único atendimento controlado, aguardando cada resposta da Eco.
10. Liberar homologação ampliada somente após confirmar ausência de duplicidade e bloqueios da Meta.

## Gate de produção

O pacote não foi instalado nem validado contra o MariaDB, o GWS, o GUP ou o WhatsApp reais durante o empacotamento. A sequência acima é obrigatória antes de publicação no canal de produção.
