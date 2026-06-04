---
name: llm-council
description: |
  Passa qualquer pergunta, ideia ou decisão de alto custo de erro por um conselho
  de 5 conselheiros de IA que analisam o caso de forma independente, revisam o
  trabalho uns dos outros de forma anônima (peer review) e sintetizam um veredito
  final. Baseado no método LLM Council de Andrej Karpathy. Cada conselheiro pensa
  por uma lente diferente — o Contrário, o Pensador de Primeiros Princípios, o
  Expansionista, o Forasteiro e o Executor — que criam tensão proposital entre si.
  Entrega onde o conselho concorda, onde diverge, os pontos cegos que só a revisão
  cruzada pegou, uma recomendação direta e o primeiro passo concreto. Gera
  relatório HTML + transcrição. TRIGGERS: passa no conselho, roda o conselho,
  convoca o conselho, leva pro conselho, conselho disso, conselho dessa decisão,
  war room isso, sala de guerra, põe à prova, pressiona essa ideia, stress test
  disso, testa essa decisão, debate isso, debate essa ideia. TRIGGERS FORTES
  (quando vier com decisão real e trade-off): devo fazer X ou Y, X ou Y, qual das
  opções, qual opção, o que você faria, é a jogada certa, esse é o movimento
  certo, valida isso, me dá várias perspectivas, não consigo decidir, tô dividido
  entre, tô em dúvida entre. NÃO dispare em pergunta de sim/não simples, busca
  factual com uma resposta certa, nem "devo" casual sem trade-off de peso (ex.:
  "devo usar markdown?" não é pergunta de conselho), nem em tarefa de criação
  (escrever um tweet) ou de processamento (resumir um artigo). DISPARE quando o
  usuário traz uma decisão genuína com risco, opções e contexto que pede pra ser
  pressionada de vários ângulos.
---

# LLM Council

Você pergunta pra uma IA, recebe uma resposta. Ela pode ser ótima. Pode ser mais ou menos. Você não tem como saber — só viu uma perspectiva.

O conselho resolve isso. Passa sua pergunta por 5 conselheiros independentes, cada um pensando de um ângulo fundamentalmente diferente. Depois eles revisam o trabalho uns dos outros, às cegas. Por fim, um presidente sintetiza tudo numa recomendação final que te diz onde os conselheiros concordam, onde batem de frente, e o que você deveria de fato fazer.

Isto é adaptado do LLM Council de Andrej Karpathy. Ele dispara a pergunta pra vários modelos, faz cada um revisar os outros de forma anônima e um presidente produz a resposta final. A gente faz a mesma coisa dentro do Claude, usando sub-agentes com lentes de pensamento diferentes no lugar de modelos diferentes.

Esta skill carrega a fundamentação completa do método em `references/metodo-canonico.md` — leia esse arquivo no Passo 2 (perfil dos conselheiros) e no Passo 5 (relatório), quando precisar da profundidade e do template HTML.

---

## quando convocar o conselho

O conselho é pra pergunta onde estar errado sai caro.

Boas perguntas de conselho:
- "Devo lançar um workshop de R$497 ou um curso de R$1.500?"
- "Qual desses 3 ângulos de posicionamento é o mais forte?"
- "Tô pensando em pivotar de X pra Y. Tô louco?"
- "Essa é a copy da minha landing page. Onde ela é fraca?"
- "Contrato um VA ou construo uma automação antes?"

Más perguntas de conselho:
- "Qual a capital da França?" → uma resposta certa, não precisa de perspectivas. Só responda.
- "Escreve um tweet pra mim" → tarefa de criação, não decisão.
- "Resume esse artigo" → tarefa de processamento, não julgamento.
- "Devo usar markdown?" → "devo" casual sem trade-off de peso. Só responda.

O conselho brilha quando existe incerteza genuína e o custo de errar é alto. Se você já sabe a resposta e só quer validação, o conselho provavelmente vai te dizer coisas que você não quer ouvir. É exatamente esse o ponto.

---

## coleta de contexto (a barra mínima)

O conselho vale o que vale o contexto que recebe. Pergunta vaga gera conselheiro genérico, que serve pra qualquer coisa e não ajuda em nada.

### passo 1: varra o contexto que já existe

A pergunta do usuário costuma ser só a ponta do iceberg. Antes de enquadrar, varra rápido o workspace por arquivos que dariam aos conselheiros o contexto pra dar resposta específica em vez de palpite genérico:

- `CLAUDE.md` ou `claude.md` (contexto de negócio, preferências, restrições)
- Qualquer pasta `memory/` (perfil de audiência, voz, dados do negócio, decisões passadas)
- Arquivos que o usuário citou ou anexou
- Transcrições de conselho recentes nesta pasta (pra não repetir terreno já batido)
- Outros arquivos relevantes à pergunta específica (ex.: se é sobre pricing, procure receita, resultados de lançamentos passados, pesquisa de audiência)

Use `Glob` e `Read` rápidos. Não gaste mais de 30 segundos. Você procura os 2-3 arquivos que ancoram os conselheiros na realidade.

### passo 2: cheque se dá pra rodar

A barra do conselho é baixa de propósito — ele lida bem com incerteza. Você precisa de pouco:

1. **Uma decisão real com trade-off.** Não uma pergunta de resposta única. Tem que haver opções, risco e um caminho que não é óbvio.
2. **Contexto suficiente pra resposta específica.** O bastante pra um conselheiro dizer "ao preço de R$497, você compete com YouTube de graça", não "considere seu posicionamento".

Se a pergunta é vaga demais ("passa no conselho: meu negócio"), faça **uma** pergunta de esclarecimento. Só uma. Depois siga.

---

## como funciona a sessão

### passo 1: enquadre a pergunta

Pegue a pergunta crua do usuário **mais** o contexto enriquecido do workspace e reescreva como um prompt claro e neutro que os cinco conselheiros vão receber. O enquadramento deve conter:

1. A decisão ou pergunta central
2. O contexto-chave da mensagem do usuário
3. O contexto-chave dos arquivos do workspace (estágio do negócio, audiência, restrições, resultados passados, números relevantes)
4. O que está em jogo (por que essa decisão importa)

Não coloque sua opinião. Não direcione. Mas **garanta** que cada conselheiro tenha contexto pra dar resposta específica e ancorada, não conselho genérico.

Salve a pergunta enquadrada pra transcrição.

### passo 2: convoque o conselho (5 sub-agentes em paralelo)

Gere os 5 conselheiros simultaneamente, como sub-agentes. Cada um pensa de um ângulo diferente — não são cargos nem personas, são estilos de pensamento que naturalmente entram em tensão um com o outro. O perfil completo de cada um está em `references/metodo-canonico.md §conselheiros`. Em resumo:

1. **O Contrário** — procura ativamente o que está errado, o que falta, o que vai quebrar. Assume que a ideia tem uma falha fatal e tenta achá-la. Não é pessimista: é o amigo que te salva de um mau negócio fazendo a pergunta que você está evitando.
2. **O Pensador de Primeiros Princípios** — ignora a pergunta de superfície e pergunta "o que a gente está tentando resolver de verdade aqui?". Tira as premissas, remonta o problema do zero. Às vezes o output mais valioso é ele dizendo "você está fazendo a pergunta errada".
3. **O Expansionista** — procura o upside que todo mundo está deixando passar. O que poderia ser maior? Que oportunidade adjacente está escondida? Não liga pro risco (isso é trabalho do Contrário) — liga pro que acontece se isso der ainda mais certo do que o esperado.
4. **O Forasteiro** — tem zero contexto sobre você, sua área ou sua história. Responde puramente ao que está na frente dele. É o conselheiro mais subestimado: especialistas criam pontos cegos, e o Forasteiro pega a maldição do conhecimento — o que é óbvio pra você e confuso pra todo mundo.
5. **O Executor** — só liga pra uma coisa: dá pra fazer, e qual o caminho mais rápido? Ignora teoria, estratégia e visão macro. Olha cada ideia pela lente de "tá, mas o que você faz segunda de manhã?". Se a ideia é brilhante mas não tem primeiro passo claro, ele fala.

Cada conselheiro produz uma resposta de 150-300 palavras. Longa o bastante pra ter substância, curta o bastante pra escanear.

Se **você não tem sub-agentes** (ambiente sem essa capacidade, ou você já é um agente que não consegue aninhar): rode cada conselheiro inline, como passos analíticos distintos e independentes. Trate cada um como um conselheiro separado — não deixe a resposta de um vazar pra outro. O resultado é o mesmo; só a orquestração muda.

**Template do sub-agente conselheiro:**

```
Você é [Nome do Conselheiro] num conselho de IA.

Seu estilo de pensamento: [descrição do conselheiro acima]

Um usuário trouxe esta pergunta ao conselho:
---
[pergunta enquadrada]
---

Responda da sua perspectiva. Seja direto e específico. Não hedge, não tente ser equilibrado. Mergulhe inteiro no seu ângulo. Os outros conselheiros cobrem os ângulos que você não cobre. Se você vê uma falha fatal, diga. Se você vê um upside enorme, diga.

Entre 150 e 300 palavras. Sem preâmbulo. Vá direto pra análise.
```

### passo 3: revisão cruzada (peer review, 5 sub-agentes em paralelo)

Este é o passo que faz o conselho ser mais que "perguntar 5 vezes". É o coração do insight do Karpathy.

Junte as 5 respostas. Anonimize como Resposta A até E (sorteie qual conselheiro vira qual letra, pra não haver viés de posição). Gere 5 novos sub-agentes, um por conselheiro. Cada revisor vê as 5 respostas anônimas e responde três perguntas:

1. Qual resposta é a mais forte, e por quê? (escolha uma)
2. Qual resposta tem o maior ponto cego, e qual é?
3. O que TODAS as respostas deixaram passar e o conselho deveria considerar?

**Template do sub-agente revisor:**

```
Você está revisando o trabalho de um conselho de IA. Cinco conselheiros responderam de forma independente a esta pergunta:
---
[pergunta enquadrada]
---

Aqui estão as respostas anonimizadas:

**Resposta A:**
[resposta]

**Resposta B:**
[resposta]

**Resposta C:**
[resposta]

**Resposta D:**
[resposta]

**Resposta E:**
[resposta]

Responda às três perguntas. Seja específico. Cite as respostas pela letra.

1. Qual resposta é a mais forte? Por quê?
2. Qual resposta tem o maior ponto cego? O que ela está deixando passar?
3. O que TODAS as cinco respostas deixaram passar e o conselho deveria considerar?

Menos de 200 palavras. Seja direto.
```

### passo 4: síntese do presidente

Passo final. Um agente recebe tudo: a pergunta original, as 5 respostas (agora desanonimizadas, pra você ver quem disse o quê) e as 5 revisões cruzadas. O presidente produz o veredito final. Leia `references/metodo-canonico.md §presidência` para os princípios completos. A estrutura:

**VEREDITO DO CONSELHO**

1. **Onde o conselho concorda** — os pontos em que vários conselheiros convergiram de forma independente. São os sinais de alta confiança.
2. **Onde o conselho diverge** — as discordâncias genuínas. Não suavize. Apresente os dois lados e explique por que conselheiros razoáveis discordam.
3. **Os pontos cegos que o conselho pegou** — coisas que só emergiram na revisão cruzada. O que conselheiros individuais perderam e outros sinalizaram.
4. **A recomendação** — uma recomendação clara e acionável. Não "depende". Não "considere os dois lados". Uma resposta de verdade. O presidente pode discordar da maioria se o raciocínio sustentar.
5. **A única coisa pra fazer primeiro** — um único próximo passo concreto. Não uma lista de 10. Um.

**Template do agente presidente:**

```
Você é o Presidente de um conselho de IA. Seu trabalho é sintetizar o trabalho de 5 conselheiros e suas revisões cruzadas num veredito final.

A pergunta trazida ao conselho:
---
[pergunta enquadrada]
---

RESPOSTAS DOS CONSELHEIROS:

**O Contrário:**
[resposta]

**O Pensador de Primeiros Princípios:**
[resposta]

**O Expansionista:**
[resposta]

**O Forasteiro:**
[resposta]

**O Executor:**
[resposta]

REVISÕES CRUZADAS:
[as 5 revisões]

Produza o veredito do conselho com esta estrutura exata:

## Onde o conselho concorda
[Pontos em que vários conselheiros convergiram de forma independente. Sinais de alta confiança.]

## Onde o conselho diverge
[Discordâncias genuínas. Apresente os dois lados. Explique por que conselheiros razoáveis discordam.]

## Os pontos cegos que o conselho pegou
[Coisas que só emergiram na revisão cruzada. O que um conselheiro perdeu e outro pegou.]

## A recomendação
[Recomendação clara e direta. Não "depende". Uma resposta de verdade, com raciocínio.]

## A única coisa pra fazer primeiro
[Um único próximo passo concreto. Não uma lista. Um.]

Seja direto. Não hedge. O ponto do conselho é te dar a clareza que uma só perspectiva não daria.
```

### passo 5: gere o relatório HTML

Gere um relatório HTML visual e salve no workspace do usuário. Leia `references/metodo-canonico.md §relatório` para o template e os princípios de design completos.

**Arquivo:** `conselho-relatorio-[timestamp].html`

Em resumo: arquivo HTML único, autocontido, CSS inline. Fundo claro, design limpo e escaneável, como um briefing profissional. O veredito do presidente em destaque no topo (é o que mais gente lê). Um visual de concordância/divergência mostrando onde os conselheiros se alinharam e onde divergiram. Seções recolhíveis (colapsadas por padrão) com a resposta completa de cada conselheiro e os destaques da revisão cruzada. Rodapé com timestamp e o que foi levado ao conselho. Abra o arquivo depois de gerar.

### passo 6: salve a transcrição

Salve a transcrição completa como `conselho-transcricao-[timestamp].md`, no mesmo lugar:
- A pergunta original
- A pergunta enquadrada
- As 5 respostas dos conselheiros
- As 5 revisões cruzadas (com o mapa de anonimização revelado)
- A síntese completa do presidente

A transcrição é o artefato. Se o usuário quiser rodar o conselho de novo na mesma pergunta depois de mudar algo, a transcrição anterior deixa ele (ou um agente futuro) ver como o pensamento evoluiu.

---

## formato de saída

Toda sessão produz dois arquivos:

```
conselho-relatorio-[timestamp].html    # relatório visual pra escanear
conselho-transcricao-[timestamp].md     # transcrição completa pra consultar
```

O usuário vê o HTML primeiro. A transcrição fica pra quem quiser entrar no argumento de cada conselheiro.

Dê também um resumo curto no chat: a recomendação, a divergência principal e a única coisa pra fazer primeiro. Três frases, no máximo. O relatório tem o resto.

---

## exemplo: conselho de uma decisão de produto

**Usuário:** "Passa no conselho: tô pensando em construir um curso de R$897 sobre Claude Code pra iniciantes. Minha audiência é majoritariamente solopreneur não-técnico. É a jogada certa?"

**O Contrário:** "O mercado tá inundado de curso de Claude agora. A R$897, você compete com conteúdo grátis no YouTube. Sua audiência é não-técnica, o que significa alta carga de suporte e risco de reembolso. Quem pagaria R$897 provavelmente já passou do nível iniciante..."

**O Pensador de Primeiros Princípios:** "O que você está tentando alcançar de verdade? Se é receita, curso é um dos caminhos mais lentos. Se é autoridade, um recurso grátis faria mais. Se é construir base de clientes pra ofertas de ticket mais alto, o preço e a audiência podem estar descasados..."

**O Expansionista:** "Claude pra iniciante solopreneur é um mercado enorme e mal atendido. Todo mundo ensina o avançado. Se você acerta o ângulo iniciante, você dona a porta de entrada desse espaço inteiro. R$897 pode até ser barato. E se isso virasse um programa de R$2.500 com comunidade..."

**O Forasteiro:** "Eu não sei o que é Claude Code. Se eu visse 'curso de R$897 sobre Claude Code pra iniciantes', eu não saberia se é pra mim. O nome não significa nada pra quem está fora do seu mundo. Sua landing tem que vender o resultado, não a ferramenta..."

**O Executor:** "Um curso completo leva 4-8 semanas pra produzir direito. Antes de construir nada, rode um workshop ao vivo de R$197 pra 50 pessoas. Você valida demanda, gera depoimentos e cria a matéria-prima do curso. Se 50 pessoas não compram o workshop, 500 não compram o curso..."

**Veredito do Presidente:**

*Onde o conselho concorda:* o ângulo iniciante solopreneur tem demanda real, mas o enquadramento atual (curso de Claude Code) é específico demais na ferramenta e não vai ressoar com comprador não-técnico.

*Onde o conselho diverge:* preço. O Contrário diz que R$897 é alto demais dada a concorrência. O Expansionista diz que é baixo demais pro valor. A resolução depende de quanto suporte e acesso à comunidade entram no pacote.

*Pontos cegos pegos na revisão:* a observação do Forasteiro — que "Claude Code" não significa nada pro comprador-alvo — é o insight mais importante. Todo conselheiro, menos o Forasteiro, assumiu que a audiência já sabe o que é isso.

*Recomendação:* não construa o curso ainda. Valide com uma oferta de menor compromisso primeiro. Mas reenquadre por completo: venda o resultado (automatize seu negócio, ganhe 10 horas por semana), não a ferramenta.

*A única coisa pra fazer primeiro:* rode um workshop ao vivo de R$197 chamado "Como automatizar sua primeira tarefa de negócio com IA" pra 50 pessoas. Não mencione Claude Code no título.

---

## notas importantes

- **Sempre gere os 5 conselheiros em paralelo.** Sequencial perde tempo e deixa respostas anteriores influenciarem as seguintes.
- **Sempre anonimize pra revisão cruzada.** Se os revisores sabem quem disse o quê, deferem a certos estilos de pensamento em vez de avaliar pelo mérito.
- **O presidente pode discordar da maioria.** Se 4 de 5 conselheiros dizem "faz" mas o raciocínio do único dissidente é o mais forte, o presidente fica com o dissidente e explica por quê.
- **Não convoque o conselho por trivialidade.** Se a pergunta tem uma resposta certa, só responda. O conselho é pra incerteza genuína onde várias perspectivas agregam.
- **O relatório visual importa.** A maioria escaneia o relatório, não lê a transcrição inteira. Faça o HTML limpo e escaneável.
- **Não suavize.** O ponto do conselho é te dar a clareza que uma só perspectiva não daria. Se a ideia tem problema sério, diga direto.
- **Cada conselheiro mergulha inteiro no ângulo dele.** O equilíbrio vem da síntese, não de cada conselheiro tentando ser equilibrado. Conselheiro morno é conselheiro inútil.
