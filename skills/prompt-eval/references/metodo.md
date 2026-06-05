# Prompt Eval — Método canônico

Material de apoio da skill `prompt-eval`. A `SKILL.md` referencia as seções daqui pelos âncoras `§objetivo-vs-subjetivo`, `§exemplos`, `§antipadroes` e `§template-output`. Se este arquivo não estiver acessível, a `SKILL.md` tem um `FALLBACK_INLINE` com a versão condensada.

---

## §objetivo-vs-subjetivo — Heurística de classificação de critério

Todo critério de eval cai em uma de duas classes. A classe define a rota de grading.

### OBJETIVO `[OBJ]` — verificável sem opinião

Um critério é objetivo quando duas pessoas, lendo o mesmo output, sempre chegam ao mesmo sim/não. Não depende de gosto.

Sinais de objetivo:
- Contagem: "cabe em X palavras", "no máximo 3 bullets", "entre 2 e 4 frases"
- Presença/ausência: "contém a palavra Y", "cita o nome do produto", "termina com pergunta"
- Lista proibida: "não usa nenhuma palavra de [delve, leverage, robust]"
- Estrutura: "tem título + 3 seções", "abre com verbo no imperativo"
- Formato: "sem emoji", "sem contração", "data no formato YYYY-MM-DD"

Rota: **grading programático** (contagem, regex, match de string). Determinístico, barato, não mente.

### SUBJETIVO `[SUBJ]` — exige julgamento humano

Um critério é subjetivo quando a resposta depende de percepção: tom, voz, elegância, persuasão, "soa como eu".

Sinais de subjetivo:
- "Soa como minha voz", "tom de autoridade", "parece humano"
- "É persuasivo", "tem gancho forte", "a abertura prende"
- "Qualidade da analogia", "clareza da explicação"

Rota: **grading humano** via AskUserQuestion, um output por vez. Nunca automatize critério subjetivo com LLM — o modelo concorda com quase tudo e o resultado mente.

### Regra de desempate

Em dúvida entre OBJ e SUBJ, classifique como **SUBJETIVO**. Grading humano em critério objetivo só custa um pouco mais de tempo; grading programático em critério ambíguo produz veredicto falso, que é pior.

### Como transformar vago em objetivo

O guardrail do S3 existe pra forçar isso. Padrão de conversão:

| Vago (rejeitar) | Objetivo (aceitar) |
|---|---|
| "Soa bem" | "Não usa nenhuma palavra da lista [X, Y, Z]" |
| "Ficou profissional" | "Sem contração, sem emoji, sem gíria" |
| "Tá direto" | "Cabe em 100 palavras ± 10%" |
| "Tem energia" | "Abre com verbo no imperativo" |
| "CTA forte" | "Termina com 1 ação concreta começando por verbo" |

---

## §exemplos — Banco de critérios bem feitos

Use como repertório no S3 pra acelerar o usuário quando ele travar.

**Tamanho e forma:**
- "Cabe em 100 palavras ± 10%"
- "No máximo 3 frases"
- "Tem exatamente 1 CTA"

**Conteúdo:**
- "Cita pelo menos 2 detalhes específicos do input"
- "Menciona o nome do produto/pessoa pelo menos 1 vez"
- "Termina com pergunta direta de próximo passo"

**Anti-AI / voz:**
- "Não usa palavras da lista: [delve, leverage, robust, seamless, unlock, navigate]"
- "Não começa com 'Olha', 'Esse projeto' ou 'No mundo de hoje'"
- "Sem paralelismo negativo do tipo 'não é X, é Y'"

**Estrutura:**
- "Abre com verbo no imperativo"
- "Tem título + corpo + fechamento, nessa ordem"
- "Cada parágrafo com no máximo 3 linhas"

---

## §antipadroes — O que invalida um eval

1. **Wizard chato** — mais de 4 AskUserQuestion seguidas sem entregar valor. O usuário desiste antes do S6.
2. **Critério vago aceito** — "soa bem" entrou sem rejeição. Todo grading subsequente vira opinião.
3. **Inputs fictícios aceitos** — "exemplo de cliente", lorem ipsum. Escondem a fragilidade que só aparece no input real.
4. **Grading subjetivo automatizado** — gradar tom/voz com regex ou LLM. Resultado mente com cara de método.
5. **Decisão sem aplicar regra** — chutar o veredicto em vez de seguir a tabela de p.p. Eval vira achismo carimbado.
6. **Gaps genéricos** — "v3 pode melhorar o tom" em vez de "v3 deve banir a abertura 'olha esse projeto'". O usuário não sabe o que mudar.
7. **Sem persistência** — fechar no chat sem salvar o .md. Em 2 semanas ninguém audita.
8. **Usuário teimoso** — ceder e pular S3/S6 na insistência. Se o usuário força, ofereça o downgrade nominal ("rodo rápido, mas o resultado não é auditável") em vez de fingir que o eval valeu.

---

## §template-output — Estrutura do arquivo `.md` final

```markdown
# Eval — [nome do prompt] — [YYYY-MM-DD]

## Hipótese
[1 frase: o que mudou de A pra B e por quê]

## Prompt A (baseline)
[texto integral]

## Prompt B (candidato)
[texto integral]

**Diff A→B:** [1 frase]

## Critérios
1. [Critério 1] — [OBJ]
2. [Critério 2] — [OBJ]
3. [Critério 3] — [SUBJ]

## Inputs
1. Caso 1 — fácil — [label]
2. Caso 2 — médio — [label]
3. Caso 3 — difícil — [label]

## Outputs
### A1 / A2 / A3
[texto]
### B1 / B2 / B3
[texto]

## Tabela de grading
| Critério | A1 | A2 | A3 | B1 | B2 | B3 |
|---|---|---|---|---|---|---|
| ... | | | | | | |

## Totais
- Prompt A: X / N (Y%)
- Prompt B: X / N (Y%)
- Diferença: +Z p.p.

## Decisão
[Adota B / Mantém A / Refaz / Roda mais casos] — regra aplicada: [qual]

## Gaps + v3 proposta
- Gap 1: [critério que B falhou + output específico]
- DIFF B → v3:
  [B] "..."
  [v3] "..."
```

A regra de decisão, em resumo: **B − A ≥ 15 p.p. → adota B** · empate (≤ 1 acerto) → mantém A · B < A → refaz · inconclusivo em N=3 → roda +2 casos.
