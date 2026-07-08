# Chatbot v393 - fluxo oficial e handoff humano

## Fonte oficial

Arquivo recebido no projeto:

```text
gabo_chatbot_revised(1).json
```

Versao declarada:

```text
v12-rc-v393-chatbot-config
```

O arquivo deve ser tratado como fonte oficial do fluxo revisado do bot.

## Regra de ativacao

O arquivo enviado declara:

```json
"engine": {
  "enabled": false
}
```

Para runtime do SAC, a importacao deve forcar:

```json
"engine": {
  "enabled": true
}
```

Sem alterar a estrutura logica do JSON.

## Fluxo inicial obrigatório

1. LGPD.
2. Nome social / forma de tratamento.
3. Contexto do atendimento.
4. Telefone quando não identificado automaticamente.
5. Cliente atual: sim/não.
6. CPF/CNPJ quando cliente já cadastrado.
7. Busca no conector SisGabo/SAC.
8. Vínculos localizados ou fallback para departments.
9. Protocolo.
10. Espera por colaborador humano.

## Template obrigatório de protocolo

```text
Seu protocolo de atendimento é: {protocolo}. Em breve um de nossos colaboradores assumirá seu atendimento. Por favor, aguarde.
```

Depois do protocolo, o atendimento pode aparecer na lista operacional do InBox.

## Regra obrigatória de assumir atendimento

Quando o operador assumir o atendimento, o backend deve persistir o handoff e enviar automaticamente a apresentação antes da primeira resposta humana digitada.

Template oficial do JSON:

```text
Olá {nome_cliente}, eu sou o {primeiro_nome_colaborador}. {saudacao_periodo}, já verifiquei aqui seu atendimento sobre {segmento_ou_assunto} e irei seguir a partir das informações fornecidas por você.
```

## Disparo correto do assume

O disparo deve ocorrer em qualquer uma das situações abaixo:

1. operador clica em assumir atendimento;
2. operador envia a primeira mensagem em atendimento ainda não assumido;
3. conversa é atribuída manualmente ao operador pelo painel.

## Ordem obrigatória quando a primeira mensagem humana for enviada

Se a conversa ainda não estiver assumida:

```text
1. Backend executa claim/handoff.
2. Persiste assigned_user_id, assigned_at, status=in_service.
3. Renderiza e envia messages.assume.
4. Registra messages.assume como mensagem de sistema/bot visível ao cliente.
5. Envia a mensagem digitada pelo operador.
6. Atualiza SLA de primeira resposta.
```

A mensagem digitada pelo operador nunca deve substituir a apresentação.
A apresentação nunca deve depender apenas do frontend.

## Variáveis obrigatórias

- `{nome_cliente}`: nome informado no fluxo ou nome resolvido pelo conector.
- `{primeiro_nome_colaborador}`: primeiro nome do operador logado/atribuído.
- `{saudacao_periodo}`: Bom dia / Boa tarde / Boa noite, conforme horário local.
- `{segmento_ou_assunto}`: resumo do vínculo, departamento, OS, contrato, serviço ou fallback selecionado.
- `{protocolo}`: protocolo gerado pelo SAC ou recebido/criado no Gabo Web Suite.

## Regras de histórico

- Mensagens de triagem anteriores ao protocolo não devem poluir o histórico operacional do colaborador.
- O colaborador deve receber contexto mastigado em `metadata.human_context`.
- O cliente deve receber a apresentação do colaborador quando o atendimento humano começar.

## Pesquisa de satisfação

Após encerramento, o bot reassume o atendimento e segue a pesquisa declarada no JSON:

1. nota do colaborador de 0 a 5;
2. solicitação atendida;
3. avaliação Gabo de 0 a 10;
4. agradecimento.
