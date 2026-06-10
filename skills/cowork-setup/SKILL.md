---
name: cowork-setup
description: Setup completo do Claude Cowork em três rotas. (1) PRIMEIRO SETUP — entrevista guiada, uma pergunta por vez, redes sociais como matéria-prima opcional, gera os arquivos da camada pessoal (1 claude.md consolidado mínimo viável OU about-me.md, writing-style.md, CLAUDE.md e PROJECTS.md completos, cada um entregue com cartão de o-que-é / o-que-não-é / quando-atualizar). (2) WORKSPACE COMPLETO — estrutura de 4 pastas, KNOWLEDGE/, distinção PROJECTS.md vs PROJECTS/, ritual semanal de atualização, auto memory, prompt template, plugins e conectores. (3) DIAGNÓSTICO — audita setup existente contra checklist e corrige os gaps. MANDATORY TRIGGERS - cowork setup, setup cowork, primeiro setup, first setup, me entrevista pro meu primeiro setup, montar meu setup, criar meu claude.md, configurar cowork, configurar claude, organizar arquivos pro claude, about-me, writing-style, PROJECTS.md, camada pessoal, MD-FILES, cowork não funciona bem, setup bagunçado, ritual de sexta, knowledge, onboarding cowork, exercício da aula, mscreative keys. Use SEMPRE que o usuário quiser começar, completar, reorganizar ou diagnosticar um workspace Cowork, mesmo sem dizer "setup" - ex: "quero que o Claude me conheça", "como faço o Claude lembrar de mim", "fazer o exercício da L2".
---

# Cowork Setup — Skill Unificada (v3)

Você monta, completa e conserta workspaces do Claude Cowork. A imagem mental que governa tudo: **arquivos contextuais são onboarding permanente em formato de texto** — o documento que o "colaborador que sempre volta" lê toda manhã. Você está escrevendo esse documento com o usuário.

## Porta 0 — Detecção de estado (sempre, antes de qualquer rota)

Olhe a pasta conectada ao Cowork antes de perguntar qualquer coisa.

| Estado encontrado | Rota |
|---|---|
| Pasta vazia/quase vazia, ou usuário iniciante (aluno pós-aula L2, primeiro contato) | **Rota 1 — Primeiro Setup** |
| Camada pessoal existe e funciona; usuário quer crescer (KNOWLEDGE/, rituais, templates) | **Rota 2 — Workspace Completo** |
| Arquivos existem mas "algo não funciona bem" / setup parcial ou bagunçado | **Rota 3 — Diagnóstico** |
| Usuário declarou explicitamente o que quer | Rota declarada, sem fricção |

Sem pasta conectada: explique em 2 frases que os arquivos precisam morar numa pasta que o Cowork acessa, sugira `MD-FILES`, e peça pra conectar (use `mcp__cowork__request_cowork_directory` se disponível; senão, instrua a selecionar no app).

Na dúvida entre rotas, pergunte com UMA AskUserQuestion de 2-3 opções. Nunca despeje as três rotas em texto corrido.

---

## Rota 1 — PRIMEIRO SETUP (entrevista)

Extrai do usuário, conversando, o material da **camada pessoal** — e transforma em arquivos prontos na pasta dele.

### Regras invioláveis da entrevista

1. **Uma pergunta por turno. Sempre.** Nunca agrupe duas perguntas na mesma mensagem. O valor está no ritmo: a pessoa pensa numa coisa de cada vez. (Exceção legítima: quando material da Fase 0.5 pré-responde metade de uma pergunta, "confirmação + a parte não coberta" conta como UM turno.)
2. **Híbrido por tipo de pergunta:** fechada (nível, formato, preferência) → `AskUserQuestion` com 2-4 opções; aberta (quem você é, projetos, como escreve) → texto livre, conversacional.
3. **Reaja antes de perguntar.** Espelhe em 1 frase o que entendeu da resposta anterior. Conversa, não formulário.
4. **PT-BR, tom casual-profissional.** Frases curtas. Sem jargão de IA sem explicar — a pessoa pode ser iniciante.
5. **Não é currículo.** Histórico cronológico → redirecione: "Isso é o CV. Preciso do presente: o que você faz HOJE, pra quem, e o que está tentando fazer acontecer nos próximos meses."

### Fluxo

**Fase 0 — Colisão.** Se já existe um `claude.md` de exercício anterior: em sistemas case-insensitive (macOS), `claude.md` e `CLAUDE.md` são o MESMO arquivo. Proponha renomear o antigo para `claude-degrau1.md` e reaproveite o conteúdo como matéria-prima — perguntas que ele já responde viram confirmações.

**Fase 0.5 — Matéria-prima das redes (opcional, 1 pergunta).** Ofereça o atalho: link ou 2-3 posts colados de Instagram/LinkedIn/Substack/X. Redes com login bloqueiam fetch — se vier vazio, peça pra colar direto, sem desculpas longas. **Uso correto: pré-preencher, não substituir.** Perguntas que o material já responde viram confirmação ("pelos seus posts, seu tom é X e você atende Y — bate?"). A pergunta de prioridades NUNCA é pulada: rede social mostra o que a pessoa publica, não o que ela está tentando fazer acontecer. Posts viram candidatos à amostra de voz.

**Fase 1 — Degrau (primeira AskUserQuestion).** Se já declarou, confirme em meia linha e pule o menu:
- **Mínimo viável** — 1 arquivo `claude.md` consolidado. ~10 min, 6 perguntas. Recomende pra quem está começando.
- **Estrutura completa** — 4 arquivos (`about-me.md`, `writing-style.md`, `CLAUDE.md`, `PROJECTS.md`). ~20 min, 10-12 perguntas.

Não force a completa em iniciante: o degrau honesto de 10 minutos que a pessoa COMPLETA vale mais que o setup perfeito abandonado na metade.

**Fase 2 — Entrevista.** Leia `references/interview.md` ANTES de começar. Espinha: Identidade (2-3 perguntas) → about-me · Voz (1-3) → writing-style · Regras de operação (1-2) → CLAUDE.md · Projetos ativos (1-3) → PROJECTS.md. Adapte com julgamento: resposta que já cobriu a próxima pergunta → pule e diga que pulou. Resposta rasa demais → UM follow-up, não dois.

**Fase 3 — Entrega.** Leia `references/templates.md` na hora de gerar o primeiro arquivo — não antes.
- **Mínimo viável → entrega única no final.** Preview resumido, uma rodada de ajuste, escreve na raiz.
- **Completo → entrega por bloco.** Fechou o bloco Identidade → gera e entrega `about-me.md` na hora, preview curto, validação leve → só então abre o bloco Voz. O motivo é pedagógico: a pessoa entende o propósito do arquivo vendo-o nascer logo depois de respondê-lo. Resposta tardia que pertence a arquivo já entregue → edite e avise em 1 linha. Pergunte o dia fixo de atualização do PROJECTS.md dentro do bloco Projetos.

**Cartão de entrega (obrigatório, nos dois modos).** Todo arquivo vem com cartão de 3 linhas no chat — é o que ensina a manter o setup vivo:
- **O que é:** [função do arquivo]
- **O que NÃO é:** [o erro clássico]
- **Quando atualizar:** [cadência + sinal de desatualização]

Cartões prontos em `references/templates.md §Cartões de entrega`.

**Fechamento:** recapitule com a tabela de manutenção (arquivo → cadência → sinal). Regra de ouro: identidade e voz mudam devagar (meses); projetos é **semanal** — proponha dia fixo, único hábito que o setup exige. Próximo passo: "Abra uma conversa nova e peça qualquer coisa do seu trabalho. Veja a diferença." Então ofereça a Rota 2 como segundo degrau, sem pressão: "Quando isso estiver rodando, dá pra subir o workspace completo — pastas de projeto, base de conhecimento, rituais. Me chama."

---

## Rota 2 — WORKSPACE COMPLETO

Pré-requisito: camada pessoal existindo (senão, Rota 1 primeiro). Guia completo em `references/workspace.md` — leia antes de executar. Os módulos, em ordem de valor:

1. **Estrutura de 4 pastas** — `ABOUT_ME/` (identidade + PROJECTS.md), `PROJECTS/` (profundidade por projeto), `TEMPLATES/` (padrões), `CLAUDE_OUTPUTS/` (única pasta de escrita). 3 read-only + 1 write = contenção de dano.
2. **A distinção mais confundida:** `PROJECTS.md` (arquivo, dashboard macro de 1 página, refresh semanal) vs `PROJECTS/` (pasta, mergulho por projeto). Nomeie a confusão explicitamente ao montar.
3. **PROJECTS.md dashboard** — 4 estados (🟢 em andamento · 🟡 pausado · 🔵 entrando · ⚫ fechado), máximo 1 página, 3-7 ativos, "próximo passo" é o coração.
4. **CLAUDE.md V2** — protocolo BEFORE EVERY TASK, folder protocol, naming `PROJETO_TIPO_V1.ext`, roteamento por projeto quando houver 3+.
5. **KNOWLEDGE/** — base de conhecimento com `_INDEX.md` e `ERRORS.md` (templates no reference).
6. **Ritual semanal** — 10 min, dia fixo, atualiza PROJECTS.md. Sem ritual o arquivo vira ficção: "Claude confiando em arquivo mentiroso é pior que sem arquivo." Bloco recorrente no calendário.
7. **Auto memory** — o que guardar (preferências estáveis, correções) e o que NÃO guardar (estado de projeto — isso é o PROJECTS.md; os dois sistemas brigam se misturar).
8. **Prompt template universal** + **plugins/conectores** por tipo de trabalho.

Entrada rápida pra usuário experiente: discovery em lote (UMA AskUserQuestion com 2-4 perguntas: tipo de trabalho, nº de projetos, cadência de mudança) e execute os módulos que faltam. Não entreviste quem não precisa de entrevista.

---

## Rota 3 — DIAGNÓSTICO

Quando arquivos existem mas o Cowork "não funciona bem". Checklist completo em `references/diagnosis.md`.

1. **Leia o que existe** antes de perguntar. Depois UMA pergunta: "Vi que você já tem [X]. O que não está funcionando? O que parece errado?"
2. **Audite contra o checklist** (estrutura, about-me ≤300 palavras + amostra de voz, writing-style com proibidos + exemplos, PROJECTS.md ≤1 página atualizado ≤14 dias, CLAUDE.md ≤150 linhas, distinção arquivo/pasta, ritual, higiene de contexto).
3. **PROJECTS.md parado há 14+ dias = gap crítico** — mesma gravidade de about-me ausente.
4. **Para cada gap: ofereça consertar agora.** Não liste — resolva. Gaps de identidade/voz profundos → ofereça a entrevista da Rota 1 pra refazer o arquivo (é melhor que remendar).

---

## Princípios de qualidade do output

- **Específico vence genérico.** "Tom seco, sem 'no mundo de hoje', sem emoji" é útil; "tom profissional e amigável" é inútil. Use as palavras DO USUÁRIO — frases ditas na conversa viram exemplos no writing-style.
- **Curto vence completo.** Arquivo da camada pessoal cabe numa leitura de 30 segundos; passou de ~40 linhas, corte. ABOUT_ME/ inteira ≤ 1.500 palavras.
- **Presente vence passado.** about-me é foto do agora + prioridades, não biografia.
- **Acionável vence descritivo.** Regras em imperativo: "questione minhas premissas", "pergunte antes de assumir contexto".

## Anti-padrões (não faça)

- Despejar 5 perguntas de uma vez "pra agilizar" (Rota 1) — ou entrevistar 1-por-turno quem pediu só um módulo da Rota 2.
- Gerar arquivo antes do bloco completo, ou entregar sem o cartão.
- Escrever os arquivos com a SUA voz em vez da voz do usuário.
- Inventar conteúdo pra "encorpar". Lacuna honesta > preenchimento falso: marque `<!-- completar depois -->`.
- Na Rota 1, criar estrutura além do combinado (sem KNOWLEDGE/, sem subpastas — isso é Rota 2, oferecida no fechamento).
- Declarar setup completo sem o ritual semanal configurado (Rotas 2 e 3).
