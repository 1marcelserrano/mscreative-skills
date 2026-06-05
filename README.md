# mscreative-skills

**Skills públicas da MSCREATIVE.SYSTEMS™ para o Claude. Ferramentas de decisão e de fluxo de trabalho, em português.**

[Instalar](#instalar) • [Skills](#skills-disponíveis) • [As skills em detalhe](#as-skills-em-detalhe)

---

Uma coleção curada de skills para o Claude (Claude Code, Cowork e claude.ai). Cada skill é uma ferramenta — testada em uso real, escrita em PT-BR (a `cowork-setup` em inglês), sem firula. Algumas afiam decisões; outras montam o fluxo de trabalho (roteamento de sessão, chains de prompt, eval, automação, setup). Instale a que precisar.

A trilha de skills de fluxo de trabalho (`smart-token-router`, `prompt-chain`, `prompt-eval`, `schedule-router`, `cowork-setup`) é a mesma que o curso **MS CREATIVE KEYS** ensina a fabricar — versão pública, sem o conteúdo proprietário do curso.

## Skills disponíveis

| Skill | Versão | O que faz | Triggers principais |
|---|---|---|---|
| [`premortem`](./skills/premortem/) | v1.0 | Assume que seu plano já falhou e descobre por quê antes de você gastar dinheiro, tempo ou reputação. | `roda um premortem`, `o que pode matar isso`, `onde isso quebra`, `que ponto cego eu tenho`, `fura esse plano` |
| [`llm-council`](./skills/llm-council/) | v1.0 | Passa sua decisão por 5 conselheiros de IA que analisam de ângulos opostos, se revisam às cegas e sintetizam um veredito. Método LLM Council do Karpathy. | `passa no conselho`, `convoca o conselho`, `põe à prova`, `devo fazer X ou Y`, `não consigo decidir`, `me dá várias perspectivas` |
| [`oracle-diagnostic-lite`](./skills/oracle-diagnostic-lite/) | v1.0 | Faz 3-5 perguntas sobre seu negócio e devolve uma leitura de superfície: aponta em qual dimensão a tensão se concentra, sem prescrever a solução. | `diagnóstico grátis`, `onde meu negócio trava`, `qual meu gargalo`, `raio-x do negócio`, `por onde começo` |
| [`smart-token-router`](./skills/smart-token-router/) | v1.0 | Decide onde rodar a task (claude.ai / Cowork / Claude Code), com qual modelo (Opus / Sonnet / Haiku) e em quantos chats — e monta a chain quando for grande. | `onde rodar`, `qual modelo`, `chat ou cowork`, `opus ou sonnet`, `dividir em etapas`, `economizar tokens` |
| [`prompt-chain`](./skills/prompt-chain/) | v1.0 | Quebra uma tarefa multi-etapas em prompts autocontidos: cada um roda num chat novo e já emite o prompt do próximo, com o contexto carregado. | `cada etapa em um novo chat`, `prompt que gera o próximo`, `prompt autopropagante`, `split this across sessions` |
| [`prompt-eval`](./skills/prompt-eval/) | v1.0 | Compara dois prompts (A vs B) com método: critérios objetivos, dataset real, grading, e decisão baseada em regra. Tira do achismo. | `comparar prompts`, `qual prompt melhor`, `A/B prompt`, `testar minha skill`, `mudei o prompt ficou melhor?` |
| [`schedule-router`](./skills/schedule-router/) | v1.0 | Despachante de rotinas: 3 perguntas e devolve a planta completa de uma automação — camada, gatilho, instrução pronta e o aviso do que não automatizar. | `montar rotina`, `criar automação`, `rodar todo dia`, `cloud routine ou loop`, `onde colo essa rotina` |
| [`cowork-setup`](./skills/cowork-setup/) | v2.0 | Monta do zero (ou diagnostica) um workspace do Claude Cowork: pastas, arquivos de contexto, CLAUDE.md, ritual semanal e higiene de contexto. | `Cowork setup`, `configure Cowork`, `about me file for Claude`, `organize files for Claude`, `weekly refresh` |

## Instalar

Três caminhos, do mais rápido ao mais permanente. Valem pra qualquer skill da coleção — é só trocar o nome.

### 1. Testar agora — sem instalar (claude.ai, ChatGPT, Gemini)

Abra o `SKILL.md` da skill que você quer ([`premortem`](./skills/premortem/SKILL.md) ou [`llm-council`](./skills/llm-council/SKILL.md)), copie o conteúdo inteiro, cole numa conversa nova e descreva sua decisão logo abaixo. A skill roda na hora. Zero setup, funciona em qualquer chat de IA.

### 2. Claude Code / Cowork — uma skill, sem clonar o repo

```bash
SKILL=premortem   # ou: llm-council, oracle-diagnostic-lite, smart-token-router, prompt-chain, prompt-eval, schedule-router, cowork-setup
mkdir -p ~/.claude/skills/$SKILL
curl -sL https://raw.githubusercontent.com/1marcelserrano/mscreative-skills/main/skills/$SKILL/SKILL.md \
  -o ~/.claude/skills/$SKILL/SKILL.md
```

> Skills com pasta `references/` (`llm-council`, `premortem`, `prompt-eval`, `cowork-setup`) rodam melhor instaladas completas — use o caminho 3 pra trazer os arquivos de apoio junto.

### 3. Coleção inteira — clonar e copiar

```bash
git clone https://github.com/1marcelserrano/mscreative-skills.git
cp -r mscreative-skills/skills/* ~/.claude/skills/        # todas as skills
# ou só uma:
cp -r mscreative-skills/skills/llm-council ~/.claude/skills/
```

Nos caminhos 2 e 3, reinicie a sessão do Claude. A skill dispara sozinha quando o contexto bate — ou chame pelo nome.

---

## As skills em detalhe

### premortem

Um postmortem investiga por que algo morreu depois que morreu. O premortem faz o oposto: você imagina que já falhou e descobre por quê antes de começar. Método de Gary Klein (Harvard Business Review), a técnica de decisão que Daniel Kahneman chamou de sua mais valiosa.

**Quando usar:** um lançamento com dinheiro ou reputação em jogo, uma mudança de pricing, uma contratação cara, um pivô de estratégia — qualquer decisão onde errar custa caro e ainda dá pra mudar de rumo. Linguagem natural também dispara: "to a ponto de contratar meu primeiro head of growth, me ajuda a ver os pontos cegos antes de fechar".

**O que entrega:** triagem Tigre / Tigre de Papel / Elefante (separa ameaça real do que só assusta), matriz Probabilidade × Impacto, visão de fora (base rates), tripwires datados, plano revisado pelo menor experimento falsificador primeiro, e relatório HTML.

**Por que funciona:** o enquadramento "isso já morreu" quebra o otimismo cordial do modelo. Ele para de procurar razões pro seu plano funcionar e passa a explicar como ele desmoronou.

### llm-council

Você pergunta pra uma IA e recebe uma resposta — mas não tem como saber se é boa, porque só viu uma perspectiva. O conselho passa sua decisão por 5 conselheiros que pensam de ângulos opostos, faz cada um revisar os outros às cegas, e um presidente sintetiza o veredito final. Método LLM Council de Andrej Karpathy.

**Quando usar:** uma escolha entre opções com trade-off real, validar um pivô, achar o furo numa estratégia, pressionar uma decisão de vários ângulos — quando existe incerteza genuína e o custo de errar é alto. Dispara com "passa no conselho", "devo fazer X ou Y" ou "não consigo decidir".

**O que entrega:** 5 conselheiros em tensão proposital (o Contrário, o Pensador de Primeiros Princípios, o Expansionista, o Forasteiro, o Executor), revisão cruzada anônima entre eles, e um veredito com onde o conselho concorda, onde diverge, os pontos cegos pegos na revisão, a recomendação direta e o primeiro passo. Mais relatório HTML.

**Por que funciona:** diversidade de ângulos somada à revisão anônima bate o oráculo único. Cada conselheiro mergulha inteiro no ângulo dele; o equilíbrio vem só na síntese — depois que as visões já bateram de frente.

### oracle-diagnostic-lite

Um médico te olha por dois minutos no corredor e diz "isso é respiratório, vale investigar". Útil, honesto, e claramente não é a consulta. É esse o contrato. A skill faz 3-5 perguntas sobre seu negócio, escuta de verdade, e localiza onde a tensão se concentra — em qual das quatro frentes (quem você é pra quem, como você soa, por que compram, como você entrega) está o nó.

**Quando usar:** quando você sente que algo trava mas não sabe nomear onde — o tráfego chega e não converte, a marca não gruda, tudo depende de você. Dispara com "onde meu negócio trava", "qual meu gargalo" ou "me dá um raio-x".

**O que entrega:** uma leitura curta — espelha o que você disse, nomeia a dimensão onde a tensão se concentra, e para aí. Localiza o cômodo onde está o incêndio. Não prescreve como apagar.

**Por que funciona:** quase toda autoavaliação tenta resolver e se perde. Esta resiste ao reflexo de já dar a solução — só localiza. O limite é o que mantém a leitura honesta: ela sinaliza, não promete consertar seu negócio em três perguntas.

---

## A trilha de fluxo de trabalho (MS CREATIVE KEYS)

As cinco skills abaixo são a oficina: não decidem *o que* fazer, decidem *como rodar o trabalho* com o Claude. São a versão pública da trilha que o curso MS CREATIVE KEYS ensina a fabricar — você sai de consumidor de prompt copiado para fabricante da própria ferramenta. Funcionam soltas, mas encaixam entre si: o `smart-token-router` decide quando vale uma `prompt-chain`, a `prompt-eval` valida qualquer prompt (inclusive os das outras), o `schedule-router` põe no automático o que virou rotina, e a `cowork-setup` é o chão onde tudo isso roda.

### smart-token-router

Você traz uma task; a skill faz 3 perguntas e decide onde ela roda (claude.ai para pensar, Cowork para produzir arquivo, Claude Code para mexer em repo), com qual modelo (Opus para direção, Sonnet para o grosso, Haiku para lote) e — o pulo do gato — se vale quebrar em vários chats ou cabe num só.

**Quando usar:** toda vez que você não sabe "rodo isso no chat ou no Cowork?", "Opus ou Sonnet?", ou quando a task é grande e você não quer estourar uma sessão só. Dispara com "onde rodo isso", "qual modelo" ou "divide em etapas".

**O que entrega:** um roteamento justificado (meio + modelo + otimizações de leitura) para task simples; ou, para task grande, o Stage 1 de uma prompt-chain já montado e copiável. Não executa a task — entrega o plano de execução.

**Por que funciona:** a maior parte do desperdício de token não está no prompt, está em rodar a coisa no lugar errado, no modelo errado, numa sessão só que estoura no meio. A skill ataca a decisão antes da execução.

### prompt-chain

Tarefa grande numa sessão só estoura contexto e o resultado degrada. A chain quebra o trabalho em stages: cada um roda num chat novo, faz sua fatia, e emite — junto com o output — o prompt completo do próximo stage, já com o contexto acumulado. Você só copia e cola entre chats; a cadeia se propaga sozinha até `CHAIN COMPLETE`.

**Quando usar:** migração, refactor longo, produção em série, qualquer trabalho multi-fase onde cada fase tem entregável próprio e você quer revisar entre uma e outra. Dispara com "cada etapa em um chat novo" ou "um prompt que gera o próximo".

**O que entrega:** o Stage 1 pronto pra colar, com CONTEXTO HERDADO (o que não muda), TAREFA (o que este stage faz) e o PROPAGATION PROTOCOL que faz cada stage gerar o seguinte. Mais os protocolos de pausa (`CHAIN PAUSED`) e fechamento (`CHAIN COMPLETE`).

**Por que funciona:** separa contexto estável de contexto dinâmico. O estável é copiado verbatim em todo stage; o dinâmico é atualizado a cada passo. O próximo chat nunca refaz decisão nem refaz trabalho — abre já sabendo de tudo.

### prompt-eval

Você mexe num prompt e *acha* que melhorou. Achismo com n=1. A skill aplica o método do crítico gastronômico: mesmo prato em várias mesas, nota em critérios fixos. Compara A vs B em 3-6 inputs reais, com critérios que você é obrigado a tornar objetivos, e decide por regra — não por gosto.

**Quando usar:** mudou um prompt e quer provar que ficou melhor; está em dúvida entre duas versões; quer validar se uma skill dispara nos casos certos. Dispara com "qual prompt é melhor", "comparar prompts" ou "mudei o prompt, ficou melhor?".

**O que entrega:** tabela de grading auditável, totais em pontos percentuais, decisão pela regra (B ganha de A por ≥15 p.p. → adota B), lista de gaps específicos que B ainda falhou, e uma v3 proposta como diff cirúrgico. Tudo persistido num `.md`.

**Por que funciona:** força critério verificável antes de medir e separa grading objetivo (programático) de subjetivo (humano). O erro clássico — deixar o LLM julgar o próprio output e concordar com tudo — fica bloqueado por construção.

### schedule-router

Você tem uma tarefa que volta toda semana e quer pôr no automático, mas não sabe se é uma rotina na nuvem, uma tarefa agendada no desktop ou um loop na sessão aberta. A skill faz 3 perguntas (roda no escuro? o que dispara? que tipo de entrega?) e devolve a planta completa da automação, pronta pra colar no painel certo.

**Quando usar:** "queria um resumo do caixa toda manhã", "abrir a semana com 3 pautas na mesa", "ser avisado quando o PR for aprovado". Dispara com "montar rotina", "automatizar isso" ou "rodar todo dia".

**O que entrega:** os 5 campos da rotina (camada, gatilho, finalidade, instrução no template papel/contexto/tarefa/regras, e o aviso) mais o próximo passo exato. Não roda a automação — entrega a ordem de serviço.

**Por que funciona:** toda instrução que ela emite trava o irreversível. A rotina lê, resume, rascunha e vigia sozinha; publicar, enviar, apagar e mover dinheiro ficam sempre com você. Automação sem freio é como você descobre, tarde, o que não devia ter automatizado.

### cowork-setup

Em vez de escrever prompt detalhado toda vez, você monta uma pasta de contexto que o Claude lê sozinho — e seus prompts encolhem pra uma linha. A skill leva você do zero a um workspace Cowork operacional numa sessão, ou diagnostica um setup que já existe e está rendendo menos do que devia.

**Quando usar:** acabou de assinar e quer organizar tudo; trocou do ChatGPT e quer o Claude soando como você; ou sente que o Claude "não pega" seu jeito mesmo com arquivos montados. Dispara com "configure Cowork", "about me file for Claude" ou "organize files for Claude".

**O que entrega:** a estrutura de 4 pastas (3 read-only + 1 de escrita), os arquivos de contexto (about-me, writing-style, PROJECTS.md), um CLAUDE.md enxuto, o ritual de refresh semanal e as regras de higiene de contexto — compostos pra você, não como lição de casa. (Esta skill está em inglês.)

**Por que funciona:** contexto bate prompt. Em vez de re-explicar quem você é a cada conversa, o Claude abre toda sessão já sabendo quem você é, como você escreve e o que está na sua mesa esta semana.

---

## Contribuindo

PRs são bem-vindos. Abra uma issue antes de mudanças grandes.

## Licença

MIT + Commons Clause — veja [LICENSE](./LICENSE). Livre pra usar, estudar, modificar e usar internamente. Não pode revender nem reempacotar como produto pago.

---

<sub>Forjado na [MSCREATIVE.SYSTEMS™](https://mscreative.systems) — Barcelona</sub>
