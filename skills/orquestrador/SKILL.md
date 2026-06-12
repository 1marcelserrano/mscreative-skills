---
name: orquestrador
description: |
  Pega um conjunto de achados, decisões ou problemas de alto custo (a saída de
  um premortem, um diagnóstico, um brief, uma lista de pendências) e transforma
  num plano executável em fases, encadeado e rastreável. Para cada fase, expõe
  o ponto de decisão (opções + recomendação), aciona a ferramenta ou skill certa
  e define o artefato concreto que sai dela. Gera a cadeia de prompts e um
  dashboard HTML de acompanhamento. O princípio: a IA ORQUESTRA e FACILITA a
  decisão; o HUMANO DECIDE. TRIGGERS: orquestra isso, monta um plano em fases,
  quebra isso em fases, vira isso numa cadeia de prompts, cria os prompts pra
  atacar isso, monta um dashboard de fases, quero acompanhar isso em fases,
  você orquestra e eu decido, transforma esse premortem (ou diagnóstico) num
  plano de execução, sequência de prompts pra resolver isso, me guia decisão a
  decisão, plano de ataque em etapas. Use SEMPRE que houver uma lista de
  problemas/decisões e o usuário quiser executá-los de forma criteriosa, fase a
  fase, mantendo o controle das escolhas. NÃO dispare para uma única tarefa
  simples e linear (isso é só fazer), nem para uma pergunta factual com resposta
  única, nem quando o usuário quer que VOCÊ decida por ele em vez de decidir ele
  mesmo.
---

# Orquestrador

A maioria dos planos morre na distância entre o diagnóstico e a execução. Você roda um premortem, um diagnóstico ou uma análise, sai com 8 problemas — e aí trava. Atacar tudo de uma vez dispersa o foco (que costuma ser um dos próprios problemas). Atacar no escuro repete o erro que o diagnóstico apontou.

O orquestrador resolve essa distância. Ele não decide por você — ele estrutura as decisões para que você decida bem, na ordem certa, sem se perder. A divisão de trabalho é fixa e explícita: **a IA orquestra e facilita; o humano decide.**

Três saídas: uma **cadeia de prompts** (um por fase, encadeados), um **dashboard de fases** (HTML autocontido, rastreável) e, em cada fase, um **artefato concreto**. Esta skill carrega o template do dashboard em `references/dashboard-template.html` — leia no Passo 5.

---

## quando orquestrar

Bons alvos:
- A saída de um premortem, de um diagnóstico, de um LLM council ou de um brief — uma lista de achados que precisa virar execução
- Um conjunto de decisões interdependentes onde a ordem importa
- Um projeto de alto custo de erro que o usuário quer conduzir mantendo o controle das escolhas

Maus alvos:
- Uma tarefa única e linear → só faça
- Pergunta factual com resposta única → responda
- O usuário quer que você decida por ele → este não é o padrão certo; ou ele decide, ou use uma skill de recomendação direta

---

## o princípio inegociável

**A IA orquestra. O humano decide.**

Em cada fase você apresenta: o que está em jogo, as opções reais, a sua recomendação fundamentada e o artefato que a decisão destrava. Você **não** avança para a próxima fase sem a decisão da fase atual — porque a decisão de uma fase quase sempre reprioriza as seguintes. Quando houver uma escolha genuína, use `AskUserQuestion` para colher a decisão; não decida no lugar do usuário e não esconda o trade-off.

Isso é o que separa orquestração de execução autônoma. O valor não é a IA fazer tudo — é a IA tornar cada decisão barata, clara e bem-sequenciada, e o humano permanecer dono do rumo.

---

## como funciona

### passo 1: receba e ancore os achados

Pegue a lista de achados/decisões a executar. Quase sempre vem de outra skill (premortem, oracle-diagnostic-lite, llm-council) ou de um documento. Releia a conversa e o workspace para não pedir o que já existe.

Bata a barra mínima — três coisas:
1. **Qual o objetivo?** O que essa execução precisa alcançar.
2. **O que é sucesso?** O resultado concreto. Sem isso, as fases não têm critério de pronto.
3. **Quais as restrições?** Tempo, recurso, quem executa. Calibra o tamanho das fases.

Se faltar, pergunte — uma de cada vez, só o necessário.

### passo 2: priorize em fases

Ordene os achados em fases. Duas regras de ordenação:
- **Decisão estrutural primeiro.** A escolha que reprioriza todas as outras (foco, direção, escopo) vira a Fase 1. Sem ela, todo o resto puxa para direções opostas.
- **Depois, por impacto × dependência.** O que destrava mais e o que outras fases precisam vem antes. Use a matriz Probabilidade × Impacto do diagnóstico, se houver.

Agrupe as fases em 3-5 macro-etapas para o usuário enxergar o arco de relance. Não force número de fases — o tamanho é o que for real para o problema.

### passo 3: desenhe cada fase

Cada fase recebe cinco campos:
1. **Objetivo** — o que essa fase resolve, em uma frase.
2. **Ponto de decisão** — a pergunta que o usuário decide. Concreta, com opções reais.
3. **Recomendação** — a sua, fundamentada, à luz do objetivo e da fase anterior. Você opina; ele decide.
4. **Ferramenta/skill acionada** — qual recurso a fase usa. Se houver skills disponíveis no ambiente, **encadeie-as** (dogfooding): a skill certa para cada trabalho. Senão, o prompt é autocontido.
5. **Artefato** — o que sai pronto da fase. Concreto, usável, não "lição de casa".

### passo 4: gere a cadeia de prompts

Escreva um prompt por fase, em sequência. Cada prompt:
- Tem um objetivo único.
- Consome o output da fase anterior — marque o ponto de inserção com um placeholder claro, ex: `[[COLE O OUTPUT DA FASE ANTERIOR]]`.
- Aciona a ferramenta/skill da fase.
- Termina especificando o artefato a produzir.

Entregue os prompts em blocos copiáveis, na ordem da cadeia, com o mapa no topo (tabela: fase / ataca / skill / consome / entrega).

### passo 5: gere o dashboard de fases

Gere um dashboard HTML autocontido a partir de `references/dashboard-template.html`. Um arquivo único, CSS e JS inline, sem dependências. Princípios:
- **Estado salvo no navegador** (localStorage) — o usuário marca cada fase (Pendente / Em decisão / Decidido / Concluído) e o progresso persiste.
- **Decisão em primeiro plano** — cada card de fase mostra o ponto de decisão, a recomendação e um campo onde o usuário registra a escolha dele.
- **Barra de progresso** e a **métrica-norte** (que sai da Fase 1) no topo.
- **Macro-etapas** como separadores visuais.
- **Painel de tripwires** ao final, se o diagnóstico os tiver produzido.
- Fundo escuro, tipografia limpa, escaneável.

Salve como `dashboard-fases-[timestamp].html` e abra depois de gerar.

### passo 6: conduza, fase a fase

Com a cadeia e o dashboard prontos, conduza. Em cada fase: apresente a decisão, recolha a escolha do usuário (`AskUserQuestion` quando houver trade-off real), gere o artefato, e só então passe à próxima. Atualize o status no dashboard ou peça ao usuário para atualizar. Nunca pule a decisão.

---

## formato de saída

Toda sessão produz:

```
cadeia-de-prompts-[timestamp].md      # os prompts encadeados, um por fase
dashboard-fases-[timestamp].html      # o painel de acompanhamento, rastreável
```

Mais, em cada fase executada, o artefato concreto daquela fase.

Dê também um resumo curto no chat: o arco das fases em uma linha, qual é a Fase 1 (a decisão estrutural) e o primeiro passo. O resto está no dashboard e na cadeia.

---

## notas importantes

- **A IA orquestra, o humano decide.** É o coração do padrão. No instante em que você decide pelo usuário, virou execução autônoma — outra coisa.
- **A decisão estrutural é a Fase 1.** Foco, direção, escopo. Ela reprioriza todo o resto; resolver depois é refazer.
- **Não avance sem a decisão da fase.** A cadeia é sequencial por um motivo: cada output alimenta o próximo prompt.
- **Encadeie as ferramentas disponíveis.** Se há skills no ambiente, use a certa para cada fase — ataca o problema E exercita as ferramentas.
- **Todo artefato é concreto.** Copy pronta, workflow pronto, calendário pronto. Nada de "considere fazer X".
- **O dashboard é o registro vivo.** É onde o usuário vê o progresso e relê as decisões que tomou. Mantenha-o em primeiro plano, não como anexo.
