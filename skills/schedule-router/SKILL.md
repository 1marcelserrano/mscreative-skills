---
name: schedule-router
description: |
  Despachante de rotinas. Faz 3 perguntas de roteamento (disponibilidade,
  gatilho, natureza da entrega) e devolve a montagem completa de uma automação —
  a camada certa, o gatilho certo, a instrução pronta no template
  papel/contexto/tarefa/regras, e o aviso do que não automatizar. Não executa a
  rotina; entrega a planta para você colar no painel certo. MANDATORY TRIGGERS:
  "montar rotina", "criar automação", "agendar tarefa", "qual camada", "cloud
  routine ou loop", "schedule-router", "rotina automática", "automatizar isso",
  "rodar todo dia", "rotina que roda sozinha", "primeira rotina", "onde colo
  essa rotina", ou qualquer pedido de automação recorrente sem camada/gatilho
  definidos. Use sempre que alguém trouxer uma tarefa repetida e quiser
  transformá-la em rotina.
version: 1.0
---

# Schedule Router

Despachante de rotinas. Você descreve a tarefa repetida; a skill decide **onde** ela roda, **o que** a dispara e **com que instrução** — e monta a planta pronta para colar.

Pense no despachante de obra: ele não levanta a parede, decide qual equipe vai e com que ordem de serviço. Aqui é igual, só que para automação — a skill não roda a rotina, entrega a ordem de serviço completa.

Não executa nada. Não publica, não envia, não apaga. Devolve a planta; você aperta o botão.

---

## QUANDO USAR

- Você tem uma tarefa que repete (toda manhã, toda semana, todo fechamento) e quer pôr no automático.
- Sabe o que quer, mas não sabe se é Cloud Routine, Desktop task ou `/loop`.
- Não sabe onde colar a instrução nem como escrevê-la para a rotina não sair do trilho.

Não use para tarefa única ("faz isso agora"). Rotina é trabalho que volta sozinho.

---

## LÓGICA DE ROTEAMENTO

Faça as 3 perguntas **nessa ordem**. Cada resposta calibra a próxima. Só emita a saída depois das três.

### P1 — DISPONIBILIDADE

> "Essa automação precisa rodar quando seu computador está desligado ou a sessão fechada?"

- **Sim, roda no escuro** → **Cloud Routine** (vive no servidor, não depende da sua máquina). Siga para P2.
- **Não, mas precisa dos arquivos da minha máquina sem eu estar na sessão** → **Desktop task** (roda local, agendada, com acesso aos seus arquivos). Pule P2, vá para P3.
- **Quero rodar agora, dentro desta conversa** → **`/loop`** (repete aqui, na sessão aberta). Pule P2, vá para P3.

### P2 — GATILHO *(só para Cloud Routine)*

> "O que dispara esse trabalho?"

- **Horário ou intervalo fixo** ("toda manhã 7h", "a cada 6h") → **Schedule**
- **Outro sistema me chama por HTTP** → **API**
- **Evento no GitHub** (PR aberto, release, merge) → **GitHub event**
- **Só quando eu clicar** → **Run manual** (Run now)

> ⚠️ Run manual significa que você ainda é o gatilho. Funciona para testar antes de ligar o schedule — não como automação permanente. Se a resposta for "só quando eu clicar", considere ligar um Schedule para o horário em que você normalmente faria isso.

### P3 — NATUREZA DA ENTREGA

> "O resultado final é:"

- **Resumo, sinal, radar de informação** → **Inteligência**
- **Rascunho de texto, pauta, sugestão** → **Produção**
- **Lista de pendências, limpeza, higiene do sistema** → **Manutenção**
- **Briefing, status, relatório de acompanhamento** → **Acompanhamento**

Com as respostas em mãos, monte a saída.

---

## TEMPLATE DE SAÍDA

Sempre nesta ordem. Sempre os 5 campos + o próximo passo.

```
CAMADA:      [Cloud Routine / Desktop task / /loop]
GATILHO:     [Schedule "toda manhã 7h" / API / GitHub event — PR aberto / Run manual / /loop a cada X min]
FINALIDADE:  [Inteligência / Produção / Manutenção / Acompanhamento]
INSTRUÇÃO:
<papel>[o especialista certo para esta tarefa — marque o que adaptar com [ajuste pro seu setor/nicho]]</papel>
<contexto>[quando roda, fuso, janela de tempo, fontes específicas]</contexto>
<tarefa>
[passos numerados, limite de itens, formato de saída]
</tarefa>
<regras>
- Use só os dados das fontes acima; cite a origem de cada item.
- Dado ausente ou não confirmado → [VERIFICAR], nunca estimativa silenciosa.
- [regra do irreversível aplicável: não envia / não publica / não apaga / não opera]
</regras>
AVISO:       [o que NÃO automatizar neste caso — a linha do irreversível desta rotina]
PRÓXIMO:     [onde executar ou colar: painel Routines / App Desktop / /loop + horário exato]
```

Regra fixa: o bloco `<regras>` sempre carrega a linha do irreversível. Toda instrução que esta skill emite trava a rotina antes de publicar, enviar, apagar ou operar.

---

## EXEMPLOS

### Exemplo 1 — Conteúdo (Produção)

Usuário: *"Toda segunda eu travo escolhendo sobre o que escrever na semana. Queria abrir a semana já com 3 pautas na mesa."*

Roteamento: P1 → roda no escuro (Cloud Routine). P2 → horário fixo (Schedule). P3 → rascunho de pauta (Produção).

```
CAMADA:      Cloud Routine
GATILHO:     Schedule "toda segunda, 6h"
FINALIDADE:  Produção
INSTRUÇÃO:
<papel>Editor de pauta que conhece minha linha editorial e meu público [ajuste pro seu nicho].</papel>
<contexto>Roda segunda 6h, fuso Brasília. Fontes: meu arquivo de temas e os 5 posts que mais salvaram nos últimos 30 dias.</contexto>
<tarefa>
1. Leia o arquivo de temas e os 5 posts de maior salvamento.
2. Proponha 3 pautas para a semana, cada uma com ângulo e a dor que resolve.
3. Saída: lista de 3, máximo 4 linhas por pauta, em nota no repo.
</tarefa>
<regras>
- Use só os dados das fontes acima; cite de qual post ou tema veio cada pauta.
- Tema sem lastro nas fontes → [VERIFICAR], nunca invente demanda.
- Não publica nada. Entrega rascunho de pauta; a escolha e o texto final são meus.
</regras>
AVISO:       Não deixe a rotina escrever nem postar o conteúdo. Ela abre a mesa; você escolhe e escreve.
PRÓXIMO:     Cole no painel Routines → New Routine → Schedule "Mon 06:00".
```

### Exemplo 2 — Financeiro (Acompanhamento)

Usuário: *"Queria um resumo do caixa toda manhã antes de eu abrir a empresa, sem precisar puxar planilha."*

Roteamento: P1 → roda no escuro (Cloud Routine). P2 → horário fixo (Schedule). P3 → briefing de status (Acompanhamento).

```
CAMADA:      Cloud Routine
GATILHO:     Schedule "todo dia útil, 6h30"
FINALIDADE:  Acompanhamento
INSTRUÇÃO:
<papel>Analista financeiro que prepara meu briefing de caixa diário [ajuste pro seu setor].</papel>
<contexto>Roda dia útil 6h30, fuso Brasília. Fonte: minha planilha de fluxo de caixa e o extrato exportado.</contexto>
<tarefa>
1. Leia saldo atual, entradas e saídas previstas para hoje.
2. Sinalize contas a vencer nas próximas 48h e qualquer saldo negativo projetado.
3. Saída: uma página — saldo, 3 alertas no máximo, em nota no repo.
</tarefa>
<regras>
- Use só os números das fontes acima; cite a data de cada lançamento.
- Valor não confirmado no extrato → [VERIFICAR], nunca estime.
- Não paga conta, não transfere, não envia cobrança. Só lê e resume.
</regras>
AVISO:       Nenhum pagamento, transferência ou cobrança no automático. A rotina lê o caixa; mover dinheiro é seu, à mão.
PRÓXIMO:     Cole no painel Routines → New Routine → Schedule "Mon–Fri 06:30".
```

### Exemplo 3 — Liderança / RH (Acompanhamento)

Usuário: *"Antes de cada 1:1 com meu time eu chego cru. Queria um preparo rápido de cada pessoa."*

Roteamento: P1 → precisa dos meus arquivos locais, sem eu estar na sessão (Desktop task). P2 → pulada. P3 → briefing de acompanhamento (Acompanhamento).

```
CAMADA:      Desktop task
GATILHO:     Schedule "toda terça, 8h" (dia dos meus 1:1)
FINALIDADE:  Acompanhamento
INSTRUÇÃO:
<papel>Apoio de liderança que prepara meu briefing de 1:1 [ajuste pro seu time].</papel>
<contexto>Roda terça 8h, fuso Brasília. Fontes: minhas notas de 1:1 anteriores e o quadro de metas de cada pessoa do time.</contexto>
<tarefa>
1. Para cada pessoa com 1:1 hoje, releia a última nota e as metas abertas.
2. Liste 2 pontos para retomar e 1 pergunta para abrir a conversa.
3. Saída: um card por pessoa, máximo 6 linhas, em nota local.
</tarefa>
<regras>
- Use só minhas notas e metas; cite a data da última conversa.
- Combinado não registrado → [VERIFICAR], nunca presuma o que ficou acordado.
- Não envia mensagem a ninguém do time. É preparo privado meu.
</regras>
AVISO:       Nada de mensagem automática para a equipe. Preparo de 1:1 é nota interna; a conversa é sua, ao vivo.
PRÓXIMO:     No App Desktop do Claude Code → aba Scheduled Tasks → New Task → Schedule "Tue 08:00". Aponte para a pasta local onde ficam suas notas de 1:1.
```

### Exemplo 4 — Operacional (rodar agora, na sessão / `/loop`)

Usuário: *"Abri um PR e quero saber assim que for aprovado, sem ficar checando a cada cinco minutos."*

Roteamento: P1 → rodar agora, dentro desta conversa (`/loop`). P2 → pulada. P3 → sinal / radar (Inteligência).

```
CAMADA:      /loop
GATILHO:     /loop a cada 5 min (dentro desta sessão)
FINALIDADE:  Inteligência
INSTRUÇÃO:
<papel>Vigia do meu PR.</papel>
<contexto>Roda nesta sessão, a cada 5 min. Fonte: o PR [número] no meu repositório.</contexto>
<tarefa>
1. Cheque o status do PR [número].
2. Se ainda aberto, responda "sem mudança" em uma linha e siga.
3. Quando aparecer aprovação ou pedido de mudança, me avise e pare o loop.
</tarefa>
<regras>
- Use só o status real do PR; nada de suposição.
- Status ambíguo → [VERIFICAR], nunca declare aprovado por conta própria.
- Não faz merge, não comenta, não fecha o PR. Só observa e avisa.
</regras>
AVISO:       Nada de merge nem comentário automático. O loop só vigia; aprovar e mergear é seu.
PRÓXIMO:     Nesta sessão, rode: /loop 5m "cheque o status do PR [número] e me avise quando mudar".
```

---

## O QUE NÃO AUTOMATIZAR

Toda saída trava o irreversível no `<regras>` e repete o limite no `AVISO`.

| Roda sozinha | Trava antes — pede você no meio |
|---|---|
| Ler, resumir, vigiar | **Publicar** post ou conteúdo |
| Rascunhar pauta, texto, briefing | **Enviar** e-mail, mensagem ou cobrança |
| Listar pendências, preparar status | **Apagar** ou sobrescrever arquivo |
| Preparar relatório interno | **Mover** dinheiro ou mexer em sistema de cliente |

Se a tarefa descrita cai na coluna da direita, a skill não a coloca no automático. Ela monta o rascunho e marca, no `AVISO`, exatamente o passo que fica com a pessoa. Rotina entrega rascunho; você aperta o botão do que não volta atrás.
