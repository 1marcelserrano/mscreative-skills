---
name: smart-token-router
description: |
  Roteador inteligente de sessões para trabalho com o Claude. Usa
  AskUserQuestion pra elicitar o contexto da task, determina Meio (claude.ai /
  Cowork / Claude Code) e Modelo (Opus / Sonnet / Haiku) com precisão, e —
  quando a task é multi-etapas — monta automaticamente uma prompt-chain com
  prompts autocontidos prontos pra copiar e colar em chats separados. Não
  executa a task; decide ONDE, COMO e EM QUANTOS chats rodá-la, minimizando
  desperdício de tokens e contexto. MANDATORY TRIGGERS: "onde rodar", "qual
  modelo", "token router", "smart router", "roteamento", "otimizar tokens",
  "chat ou cowork", "opus ou sonnet", "economizar sessão", "dividir em etapas",
  "prompt chain", "multi-step", "cada etapa em chat novo", ou qualquer task nova
  sem meio/modelo definidos. Use sempre que alguém trouxer uma task sem contexto
  de execução definido.
version: 1.0
---

# Smart Token Router

Roteador de sessão com elicitação ativa. Não executa tasks — determina **onde**, **como** e **em quantos chats** rodá-las, minimizando desperdício de tokens e contexto.

Integra dois sistemas:
- **Roteamento** — decide Meio, Modelo e otimizações de leitura
- **Prompt Chain** — quando a task é multi-etapas, monta uma cadeia de prompts autocontidos (um por chat), com propagação automática de contexto entre sessões (ver a skill `prompt-chain`)

---

## FASE 1 — ELICITAÇÃO (AskUserQuestion)

Antes de qualquer roteamento, faça **3 perguntas em sequência** usando o `AskUserQuestion`. Não pule etapas — cada resposta calibra a decisão seguinte.

### Pergunta 1 — Tipo de task

> "Qual é o tipo da sua task?"

Opções (adapte ao contexto do usuário):
- 📝 Criação de conteúdo (copy, artigo, post, email)
- 🎯 Estratégia / negócio (posicionamento, pricing, diagnóstico, decisão)
- 🎨 Visual / design (identidade, prompt de imagem, design system)
- ⚙️ Operacional / técnico (código, pipeline, tracking, commit, refactor, scheduling)
- 🔬 Pesquisa / análise (investigação, síntese, comparação)

### Pergunta 2 — Complexidade e escopo

> "Como você descreveria o tamanho desta task?"

Opções:
- ⚡ Rápida — entregável único, menos de 15 min
- 📦 Média — 1–3 entregáveis, menos de 1 hora
- 🏗️ Grande — múltiplas fases, mais de 1 hora ou vários entregáveis interdependentes
- 🔄 Recorrente — task que se repete periodicamente (considere a skill `schedule-router`)

### Pergunta 3 — Contexto disponível

> "Você tem arquivos ou materiais no workspace para esta task?"

Opções:
- 📁 Sim, tenho arquivos relevantes no workspace
- 💬 Não, é tudo na cabeça / vou descrever agora
- 🔗 Tenho links / referências externas
- 📋 Tenho um briefing ou doc separado para compartilhar

---

## FASE 2 — ROTEAMENTO

Com as 3 respostas em mãos, tome as 4 decisões abaixo.

### DECISÃO 1 — MEIO

```
A task precisa LER arquivos do workspace ou CRIAR deliverables persistentes?
  ├── Não → claude.ai (chat web)
  └── Sim ↓
       A task envolve código de repositório (refactor, commit, feature técnica)?
         ├── Sim → CLAUDE CODE (terminal)
         └── Não → COWORK (desktop app)
```

| Tipo de task | Meio |
|---|---|
| Brainstorm, Q&A, decisão, rascunho conceitual | claude.ai |
| Criar .md, .docx, .pptx; conteúdo persistente; rodar skills | Cowork |
| Mexer em repositório, git commit, refactor, feature técnica | Claude Code |

### DECISÃO 2 — MODELO

```
A task define DIREÇÃO estratégica (decisão de produto, síntese complexa, arquitetura)?
  ├── Sim → OPUS
  └── Não ↓
       A task é TRIVIAL (rename, extract, lint, format em lote)?
         ├── Sim → HAIKU
         └── Não → SONNET (default)
```

Referência de custo mental: Opus é o tier caro. Reserve pra decisões de direção e síntese de alto impacto. Haiku pra lote e rotina. Sonnet pro resto.

### DECISÃO 3 — COMPLEXIDADE → CHAIN OU SESSÃO ÚNICA?

Este é o ponto de bifurcação central da skill:

```
Escopo respondido na Pergunta 2 foi "Grande" (múltiplas fases)?
  ├── Não → SESSÃO ÚNICA → emitir roteamento simples (Fase 3A)
  └── Sim ↓
       A task tem etapas com deliverables distintos e verificáveis?
         ├── Não → SESSÃO ÚNICA (overhead da chain não compensa)
         └── Sim → PROMPT CHAIN → montar cadeia (Fase 3B)
```

**Critério de chain:** a task vale uma chain quando tem 2 ou mais fases onde cada fase produz um entregável concreto E a fase seguinte depende do output da anterior.

### DECISÃO 4 — OTIMIZAÇÕES DE LEITURA

Para cada arquivo que a task vai tocar:
- Arquivo grande com seções nomeadas? → leia o range/seção específica, não o arquivo inteiro
- Arquivo > 100 linhas sendo editado parcialmente? → **Edit, não Write**
- Doc muito longo usado entre sessões? → sugerir split em MASTER + DETALHES
- "Leia minha pasta inteira" → substituir por leitura cirúrgica dos arquivos-chave

---

## FASE 3A — OUTPUT: SESSÃO ÚNICA

Use este formato quando a task couber em um único chat:

```
## ROTEAMENTO PROPOSTO

**Task:** [parafrasear em 1 linha]

**Meio:** [claude.ai | Cowork | Claude Code]
  → Porque: [1 linha]

**Modelo:** [Opus | Sonnet | Haiku]
  → Porque: [1 linha]

**Otimizações:**
- [otimização 1 com arquivo/range específico]
- [otimização 2]

**Custo estimado:** [baixo / médio / alto] · **Duração estimada:** [XX min]

**Próximo passo:** Abra [MEIO] e inicie com [MODELO].
```

---

## FASE 3B — OUTPUT: PROMPT CHAIN

Use este formato quando a task exigir múltiplos chats. (A skill `prompt-chain` cobre o protocolo completo de propagação — esta seção é o resumo operacional.)

### Passo 1 — Decomponha em 2–6 stages

**Heurísticas de corte:**
- Cada stage tem um deliverable concreto e verificável
- Um stage não depende do estado interno do anterior — só de arquivos e decisões registradas
- Priorize: P0 (bloqueadores) → P1 (alto impacto) → P2 (polish)
- Teste dos 10 min: stage < 5 min → junte com vizinho; > 30 min → quebre
- Máximo 6 stages. Acima disso, re-agrupe.

**Roteamento por stage:** cada stage pode ter Meio/Modelo diferentes. Inclua essa decisão no cabeçalho de cada stage.

### Passo 2 — Extraia contexto estável

Antes de redigir os prompts, separe:
- **Objetivo final** — o que significa "chain completa"?
- **Workspace** — caminho absoluto + convenções
- **Restrições que não mudam** — design system, compliance, voz da marca
- **Decisões já tomadas** — o que não será reaberto
- **Ambiente alvo por stage** — Cowork / Code / claude.ai

Esse conjunto vai na seção `CONTEXTO HERDADO` de todos os stages, inalterado.

### Passo 3 — Redija o Stage 1 (prompt-semente)

Use o template canônico abaixo. Este é o único prompt que o usuário cola manualmente; os demais a chain gera sozinha.

````markdown
# STAGE N/TOTAL — [NOME_CURTO]
# Chain: "[NOME DA CHAIN]"
# Roteamento: [Meio] · [Modelo]

## CHAIN META
- Total stages: TOTAL
- Current stage: N/TOTAL
- (todos os stages resumidos em uma linha cada)

## WORKSPACE
Absolute path: `[caminho absoluto]`
Ambiente alvo: [Claude Code / Cowork / claude.ai]

## CONTEXTO HERDADO — LEITURA OBRIGATÓRIA

### Objetivo da chain
[Enunciado único do que significa chain completa]

### Decisões já tomadas
- [decisão 1 — não reabrir]

### Estado atual auditado ([YYYY-MM-DD])
- ✅ EXISTE: [arquivos criados por stages anteriores]
- ❌ NÃO EXISTE: [arquivos faltantes]

### [Contexto estável: design system / voz / compliance / etc.]
[Blocos literais, copiados verbatim em todos os stages]

## TAREFA DESTE STAGE
1. [ação concreta com critério de "feito"]

## RESTRIÇÕES
- [o que NÃO fazer neste stage]

## DELIVERABLES
1. [arquivo/output 1]
N. **OBRIGATÓRIO**: bloco `### PRÓXIMO PROMPT — STAGE N+1` ao final

## PROPAGATION PROTOCOL — CRÍTICO
Ao final da sua resposta, emita um bloco de código markdown com o prompt completo e autocontido para Stage N+1. O próximo chat terá ZERO memória deste. O prompt de Stage N+1 deve:
- Abrir com `# STAGE N+1/TOTAL — [NOME]` e `# Roteamento: [Meio] · [Modelo]`
- Copiar verbatim CHAIN META, WORKSPACE e todo CONTEXTO HERDADO estável
- Atualizar "Decisões já tomadas" e "Estado atual auditado" com o que você acabou de fazer
- Substituir TAREFA pela lista de ações do Stage N+1
- Incluir o mesmo PROPAGATION PROTOCOL para Stage N+2 (ou FINAL TERMINATION se N+1 for o último)

Se este stage não puder ser completado (bloqueio, ambiguidade), emita `### CHAIN PAUSED` com pergunta direta ao usuário.
````

### Passo 4 — Entregue ao usuário

Apresente o Stage 1 em bloco de código copiável, com instruções de uso:

```
──────────────────────────────────────────
▶ COMO USAR ESTA CHAIN

1. Abra um chat novo em [MEIO] com [MODELO]
2. Cole o bloco STAGE 1 abaixo
3. Ao final da resposta, você verá o bloco "### PRÓXIMO PROMPT — STAGE 2"
4. Copie esse bloco e cole em um NOVO chat
5. Repita até aparecer "### CHAIN COMPLETE"

Stages desta chain:
  Stage 1 — [nome] → [Meio/Modelo]
  Stage 2 — [nome] → [Meio/Modelo]
  ...

Custo estimado total: [baixo/médio/alto]
──────────────────────────────────────────
```

---

## PROTOCOLOS DE TRANSIÇÃO DA CHAIN

### CHAIN PAUSED (bloqueio)

Quando um stage não pode ser completado sem input humano:

```markdown
### CHAIN PAUSED

**O que foi feito:** [...]
**Bloqueio:** [o que impede progressão]
**Pergunta para o usuário:** [direta, única, com opções quando possível]
**Como retomar:** Responda à pergunta. Em seguida, copie este mesmo prompt de STAGE N em chat novo, acrescentando no início uma seção "## DECISÃO DO USUÁRIO" com a resposta.
```

Pausar é sempre preferível a adivinhar. Uma adivinhação no stage N contamina todos os seguintes.

### CHAIN COMPLETE (último stage)

```markdown
### CHAIN COMPLETE

**Objetivo da chain:** [enunciado original da CHAIN META]
**Entregáveis finais:** [arquivos + caminhos]
**Decisões registradas durante a chain:** [por stage]
**Próximos passos fora da chain:** [deploy, revisão humana, publicação — se houver]
```

---

## ANTI-PATTERNS A DETECTAR E CORRIGIR

| Código | Sintoma | Correção |
|---|---|---|
| AP-01 | Task técnica rodando em Cowork sem repo | Mover para Claude Code |
| AP-02 | Brainstorm rodando em Cowork desnecessariamente | Mover para claude.ai |
| AP-03 | Opus em task trivial (rename, format) | Downgrade para Haiku |
| AP-04 | Haiku em task estratégica | Upgrade para Sonnet/Opus |
| AP-05 | "Leia minha pasta inteira" | Substituir por leitura cirúrgica |
| AP-06 | Write em doc > 100 linhas para mudar 2 linhas | Trocar por Edit |
| AP-07 | Doc > 500 linhas sem split | Propor MASTER + DETALHES |
| AP-08 | Task grande executada toda em 1 chat | Propor chain com stages separados |
| AP-09 | Chain com > 6 stages | Re-agrupar stages; máximo 6 |
| AP-10 | Stage sem deliverable verificável | Redefinir DoD antes de continuar |

---

## CHECKLIST PRÉ-ENTREGA

Antes de entregar qualquer roteamento:

- [ ] Elicitação completa (3 perguntas respondidas)
- [ ] Meio justificado em 1 linha
- [ ] Modelo calibrado com a complexidade real da task
- [ ] Decisão chain vs. sessão única explicitada
- [ ] Se chain: Stage 1 copiável e autocontido; instruções de uso acima do bloco
- [ ] Se chain: roteamento (Meio/Modelo) embutido no cabeçalho de cada stage
- [ ] Pelo menos 1 otimização de leitura identificada
- [ ] Custo estimado informado
