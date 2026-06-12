# mscreative-skills

**Skills públicas da MSCREATIVE.SYSTEMS™ para o Claude. Ferramentas de decisão, em português.**

[Instalar](#instalar) • [Skills](#skills-disponíveis) • [As skills em detalhe](#as-skills-em-detalhe)

---

Uma coleção curada de skills para o Claude (Claude Code, Cowork e claude.ai). Cada skill é uma ferramenta de pensamento — testada em uso real, escrita em PT-BR, sem firula. Instale a que precisar.

## Skills disponíveis

| Skill | Versão | O que faz | Triggers principais |
|---|---|---|---|
| [`premortem`](./skills/premortem/) | v1.0 | Assume que seu plano já falhou e descobre por quê antes de você gastar dinheiro, tempo ou reputação. | `roda um premortem`, `o que pode matar isso`, `onde isso quebra`, `que ponto cego eu tenho`, `fura esse plano` |
| [`llm-council`](./skills/llm-council/) | v1.0 | Passa sua decisão por 5 conselheiros de IA que analisam de ângulos opostos, se revisam às cegas e sintetizam um veredito. Método LLM Council do Karpathy. | `passa no conselho`, `convoca o conselho`, `põe à prova`, `devo fazer X ou Y`, `não consigo decidir`, `me dá várias perspectivas` |
| [`oracle-diagnostic-lite`](./skills/oracle-diagnostic-lite/) | v1.0 | Faz 3-5 perguntas sobre seu negócio e devolve uma leitura de superfície: aponta em qual dimensão a tensão se concentra, sem prescrever a solução. | `diagnóstico grátis`, `onde meu negócio trava`, `qual meu gargalo`, `raio-x do negócio`, `por onde começo` |
| [`nem-parece-ia`](./skills/nem-parece-ia/) | v1.0 | Revisa textos em PT-BR para remover cara de IA, lero-lero corporativo, falsa profundidade e cadência robótica sem apagar a voz do autor. | `não parecer IA`, `tira o lero-lero`, `deixa mais natural`, `revisa esse texto`, `humaniza em pt-br` |
| [`geo-content-brief`](./skills/geo-content-brief/) | v1.0 | Transforma um keyword num brief que faz a página ranquear no Google e ser citada por AI Overviews, ChatGPT e Perplexity (GEO/AEO). Bimodal: brief para o redator ou gate de pré-publicação. | `preciso de um brief`, `otimizar para AI Overviews`, `vai ser citado por IA?`, `roda o gate`, `geo brief` |
| [`cowork-setup`](./skills/cowork-setup/) | v3.0 | Monta, completa e conserta seu workspace do Claude Cowork em 3 rotas: primeiro setup por entrevista (uma pergunta por vez), workspace completo (KNOWLEDGE/, ritual semanal) e diagnóstico do que não funciona. | `me entrevista pro meu primeiro setup`, `setup cowork`, `criar meu claude.md`, `cowork não funciona bem`, `ritual de sexta`, `quero que o Claude me conheça` |
| [`orquestrador`](./skills/orquestrador/) | v1.0 | Pega os achados de um premortem, diagnóstico ou brief e vira um plano em fases: cadeia de prompts encadeados + dashboard HTML de acompanhamento. A IA orquestra e facilita; você decide. | `orquestra isso em fases`, `monta um plano em fases`, `vira isso numa cadeia de prompts`, `dashboard de fases`, `você orquestra e eu decido` |

## Instalar

Três caminhos, do mais rápido ao mais permanente. Valem pra qualquer skill da coleção — é só trocar o nome.

### 1. Testar agora — sem instalar (claude.ai, ChatGPT, Gemini)

Abra o `SKILL.md` da skill que você quer ([`premortem`](./skills/premortem/SKILL.md), [`llm-council`](./skills/llm-council/SKILL.md), [`oracle-diagnostic-lite`](./skills/oracle-diagnostic-lite/SKILL.md), [`nem-parece-ia`](./skills/nem-parece-ia/SKILL.md), [`geo-content-brief`](./skills/geo-content-brief/SKILL.md), [`cowork-setup`](./skills/cowork-setup/SKILL.md) ou [`orquestrador`](./skills/orquestrador/SKILL.md)), copie o conteúdo inteiro, cole numa conversa nova e descreva sua demanda logo abaixo. A skill roda na hora. Zero setup, funciona em qualquer chat de IA.

### 2. Claude Code / Cowork — uma skill, sem clonar o repo

```bash
SKILL=premortem   # ou: llm-council, oracle-diagnostic-lite, nem-parece-ia, geo-content-brief, cowork-setup, orquestrador
mkdir -p ~/.claude/skills/$SKILL
curl -sL https://raw.githubusercontent.com/1marcelserrano/mscreative-skills/main/skills/$SKILL/SKILL.md \
  -o ~/.claude/skills/$SKILL/SKILL.md
```

> Skills com pasta `references/` (como a `llm-council` e a `cowork-setup`) rodam melhor instaladas completas — use o caminho 3 pra trazer os arquivos de apoio junto.

### 3. Coleção inteira — clonar e copiar

```bash
git clone https://github.com/1marcelserrano/mscreative-skills.git
cp -r mscreative-skills/skills/* ~/.claude/skills/        # todas as skills
# ou só uma:
cp -r mscreative-skills/skills/nem-parece-ia ~/.claude/skills/
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

### nem-parece-ia

Uma revisão editorial para textos em português do Brasil que estão corretos, mas soam genéricos, inflados, artificiais ou parecidos com saída de IA. A skill corta abertura vazia, jargão corporativo, falsa profundidade, contraste performático, sujeito abstrato e ritmo robótico.

**Quando usar:** posts, artigos, e-mails, textos institucionais, landing pages, propostas, apresentações e relatórios que precisam soar mais naturais, específicos e brasileiros. Dispara com "não parecer IA", "tira o lero-lero", "deixa mais natural" ou "revisa esse texto".

**O que entrega:** diagnóstico dos vícios dominantes, versão revisada do texto, tabela de principais mudanças quando útil, e calibração por registro: social, ensaio, e-mail, institucional, técnico, acadêmico, comercial ou criativo.

**Por que funciona:** a maioria das revisões tenta só trocar palavras. Esta separa o problema em frases, estruturas, ritmo, registro e exemplos. O resultado não é "texto humano fake"; é texto mais claro, mais específico e menos automático.

### geo-content-brief

A busca parou de terminar num clique e passou a terminar numa resposta gerada. Esta skill transforma um keyword num brief que faz a página ranquear no Google e — mais que isso — ser *citada* dentro de AI Overviews, ChatGPT, Perplexity e Gemini. Baseada no estudo GEO de Princeton (SIGKDD 2024) e em dados de citação de 2025-2026.

**Quando usar:** quando você vai escrever, ou já escreveu, uma página que precisa ser encontrada e citada por IA — um artigo, uma página de produto, uma base de conhecimento. Dispara com "preciso de um brief de conteúdo", "como otimizo isso pra AI Overviews", "esse artigo vai ser citado?" ou "roda o gate".

**O que entrega:** é bimodal. No modo Estratégia, um brief de 8 campos pronto pro redator — answer block, mapa de H2 a partir das PAA, edge defensável, sinal de E-E-A-T. No modo Produção, diagnostica um rascunho ou URL que já existe: reescreve o answer block, torna cada seção autocontida, gera o schema FAQPage e a entrada de llms.txt, e roda um gate de 5 pontos antes de publicar.

**Por que funciona:** SEO clássico te faz clicável; GEO/AEO te faz citável. A skill ataca o que ganha citação segundo a evidência — resposta direta nos primeiros 150 tokens (de onde sai ~55% das citações), seções que se sustentam isoladas (passage ranking) e dado próprio. Estrutura, não floreio.

### cowork-setup

Todo chat novo com IA começa do zero: você reexplica quem é, o que faz, como escreve. O cowork-setup resolve isso de ponta a ponta — e escolhe o caminho certo pro seu estado. Pasta vazia? Te entrevista, uma pergunta por vez, podendo partir das suas redes sociais como matéria-prima, e gera os arquivos que o Claude lê toda conversa: o documento de onboarding do colaborador que sempre volta. Camada pessoal pronta? Sobe o workspace completo. Algo não funciona? Diagnostica e conserta.

**Quando usar:** no primeiro contato com o Claude Cowork ou Claude Code ("me entrevista pro meu primeiro setup", "quero que o Claude me conheça"); pra crescer o workspace (KNOWLEDGE/, ritual semanal, plugins); ou quando as respostas vêm genéricas e desatualizadas ("meu cowork não funciona bem").

**O que entrega:** na rota de primeiro setup, dois degraus — mínimo viável (1 `claude.md` consolidado, ~10 minutos) ou estrutura completa (`about-me.md`, `writing-style.md`, `CLAUDE.md`, `PROJECTS.md`, entregues um por bloco), cada arquivo com cartão de 3 linhas: o que é, o que NÃO é, quando atualizar. Na rota de workspace, a estrutura de pastas, a base KNOWLEDGE/ e o ritual semanal de 10 minutos. Na de diagnóstico, auditoria contra checklist com conserto na própria sessão.

**Por que funciona:** quase todo setup morre porque a pessoa tenta preencher 4 templates de uma vez e abandona na metade — a entrevista inverte o esforço, e cada arquivo nasce logo depois do bloco que o alimenta. E quase todo setup que sobrevive apodrece sem manutenção — por isso toda rota termina ensinando o hábito que mantém os arquivos vivos. Unificação (v3, jun/2026) das antigas `first-setup` e `cowork-setup` V2, validada por eval A/B sem regressão.

### orquestrador

Você roda um premortem, um diagnóstico ou um council e sai com 8 problemas — e trava na distância entre o diagnóstico e a execução. Atacar tudo de uma vez dispersa o foco (que costuma ser um dos próprios problemas); atacar no escuro repete o erro apontado. O orquestrador fecha essa distância: transforma a lista de achados num plano em fases, encadeado e rastreável.

**Quando usar:** depois de qualquer skill ou análise que cospe uma lista de decisões — premortem, oracle-diagnostic-lite, llm-council, um brief, um backlog de pendências de alto custo. Dispara com "orquestra isso em fases", "vira isso numa cadeia de prompts", "monta um dashboard de fases" ou "você orquestra e eu decido".

**O que entrega:** três saídas — uma **cadeia de prompts** (um por fase, encadeados, cada um acionando a ferramenta/skill certa), um **dashboard HTML** de acompanhamento (autocontido, estado salvo no navegador, status e decisão por fase), e em cada fase um **artefato concreto**. A decisão estrutural (foco/direção) sempre vira a Fase 1, porque reprioriza todo o resto.

**Por que funciona:** o princípio é inegociável — a IA **orquestra e facilita**, o humano **decide**. Em cada fase você recebe a decisão, as opções e a recomendação; a escolha é sua e fica registrada. O valor não é a IA fazer tudo: é tornar cada decisão barata, clara e bem-sequenciada, com você dono do rumo.

---

## Contribuindo

PRs são bem-vindos. Abra uma issue antes de mudanças grandes.

## Licença

MIT + Commons Clause — veja [LICENSE](./LICENSE). Livre pra usar, estudar, modificar e usar internamente. Não pode revender nem reempacotar como produto pago.

---

<sub>Forjado na [MSCREATIVE.SYSTEMS™](https://mscreative.systems) — Barcelona</sub>
