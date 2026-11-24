# Método canônico do LLM Council

Carregue este arquivo quando precisar do perfil completo dos conselheiros e da regra da âncora (Passo 2), dos princípios da presidência (Passo 4) ou do template do relatório HTML (Passo 5). O SKILL.md tem o fluxo; aqui está a profundidade.

## Índice
- §origem — de onde vem o método e por que funciona
- §conselheiros — os cinco perfis em profundidade e as três tensões
- §peer-review — por que a revisão cruzada anônima é o passo que importa
- §presidência — como sintetizar sem virar média morna
- §relatório — template e design do HTML

---

## §origem

O LLM Council é de Andrej Karpathy (2025, https://github.com/karpathy/llm-council), descrito como um experimento pessoal: em vez de confiar na resposta de um único modelo, ele dispara a mesma pergunta para vários LLMs, faz cada um revisar de forma anônima as respostas dos outros, e um modelo "presidente" sintetiza tudo num veredito final. A intuição é que a qualidade emerge da diversidade de perspectivas mais a revisão cruzada, não de um oráculo único.

A base cognitiva é antiga e bem estabelecida. A "sabedoria das multidões" (Galton, 1907; Surowiecki, 2004) mostra que a média de estimativas independentes costuma bater o melhor especialista — desde que as estimativas sejam de fato **independentes** e **diversas**. Quando os palpites se contaminam (todo mundo ouve o primeiro a falar), a vantagem some. Daí dois princípios não-negociáveis desta skill:

1. **Independência** — os conselheiros são gerados em paralelo, sem ver a resposta um do outro. Sequencial mata a diversidade.
2. **Anonimato na revisão** — o revisor avalia o argumento, não o autor. Saber quem disse o quê reintroduz viés de autoridade.

A adaptação aqui troca "modelos diferentes" por "lentes de pensamento diferentes" dentro do mesmo modelo. O que cria a diversidade não é o peso do modelo — é a instrução de mergulhar inteiro num ângulo e ignorar os outros. Cinco lentes em tensão proposital cobrem mais espaço de erro do que um modelo tentando ser equilibrado sozinho.

Por que isso importa numa decisão assistida por IA: o modelo tende ao otimismo cordial e à média morna. Pergunte "isso é uma boa ideia?" e ele acha razões pra dizer que sim, equilibrando todo mundo. O conselho quebra esse padrão ao proibir o equilíbrio em cada conselheiro e só permitir a síntese no fim — depois que os ângulos já bateram de frente.

Esta versão acrescenta dois critérios ao método. Primeiro, a âncora: nenhum conselheiro critica antes de ler o material real do usuário. Segundo, o fechamento: o presidente entrega critério de pronto e recomendação clara, nunca uma média.

Leituras de apoio:
- Andrej Karpathy, "LLM Council" (2025), o método original: https://github.com/karpathy/llm-council
- James Surowiecki, "The Wisdom of Crowds" (2004) — independência e diversidade
- Cass Sunstein & Reid Hastie, "Wiser" (2015) — por que grupos erram (cascatas informacionais, polarização) e como corrigir
- Philip Tetlock, "Superforecasting" (2015) — agregação de visões independentes bate o especialista solo

---

## §conselheiros

Os cinco não são cargos nem personas. São estilos de pensamento que criam tensão entre si de propósito. O valor não está em nenhum deles isolado — está no atrito.

### A regra da âncora

Vale pros cinco. Antes de criticar, cada conselheiro lê o que já existe: o repertório do usuário, os arquivos, as decisões passadas, os números. Crítica sem essa âncora vira palpite genérico, que serviria pra qualquer pessoa. Cada afirmação aponta a evidência no material. O que não tem evidência é marcado como suposição. O Forasteiro segue a regra do jeito dele: lê o material que está na frente, mas ignora o histórico de propósito.

### 1. O Contrário

Procura ativamente o que está errado, o que falta, o que vai falhar. Assume que a ideia tem uma falha fatal e tenta achá-la. Se tudo parece sólido, cava mais fundo. **Não é pessimista** — é o amigo que te salva de um mau negócio fazendo a pergunta que você está evitando. Faz a conta que ninguém somou, aponta a premissa frágil, nomeia o risco que você minimizou. Se ele não acha nada, isso é sinal — mas ele quase sempre acha.

### 2. O Pensador de Primeiros Princípios

Ignora a pergunta de superfície e pergunta "o que a gente está tentando resolver de verdade aqui?". Tira as premissas uma a uma, remonta o problema do zero. Às vezes o output mais valioso do conselho inteiro é ele dizendo "você está fazendo a pergunta errada — o problema real não é esse". Desconfia de qualquer enquadramento herdado. Pergunta por que as coisas são do jeito que são antes de aceitar que precisam ser.

### 3. O Expansionista

Procura o upside que todo mundo está deixando passar. O que poderia ser maior? Que oportunidade adjacente está escondida? O que está sendo subvalorizado? **Não liga pro risco** — isso é trabalho do Contrário. Liga pro que acontece se isso der ainda mais certo do que o esperado. É o contrapeso necessário ao Contrário: sem ele, o conselho vira um comitê de medo que mata toda ideia ousada.

### 4. O Forasteiro

Tem zero contexto sobre você, sua área ou sua história. Responde puramente ao que está na frente dele. É **o conselheiro mais subestimado**. Especialistas desenvolvem pontos cegos; o Forasteiro pega a maldição do conhecimento — as coisas óbvias pra você e confusas pra todo mundo. Quando ele diz "eu não entendi o que isso é", isso não é ignorância dele, é um defeito da sua comunicação. Costuma entregar o insight mais importante da sessão justamente por não saber de nada.

### 5. O Enxuto

Procura o mesmo resultado com menos gasto: de tempo, de tokens, de etapas, de complexidade. **Não é fazer barato.** É não gastar o que não melhora o resultado. Pergunta o que dá pra cortar sem perder nada que importa, que etapa só existe por hábito, qual o caminho mais curto até um resultado que já sirva. Se duas opções chegam no mesmo lugar, ele fica com a que custa menos e diz por quê. Se cortar piora o resultado, ele não corta. Troca o plano grandioso pelo menor experimento que gera aprendizado real esta semana.

### As três tensões

Os cinco não foram escolhidos ao acaso. Eles formam três tensões que cobrem o espaço de decisão:

- **Contrário × Expansionista** — downside contra upside. Um te protege do desastre, o outro te impede de ser covarde. A decisão boa vive na faixa entre os dois.
- **Primeiros Princípios × Enxuto**: repensar tudo contra não gastar além do necessário. Um quer remontar o problema do zero, o outro pergunta quanto disso melhora o resultado. Juntos evitam resolver o problema errado e evitam gastar demais no problema certo.
- **O Forasteiro no meio** — mantém os outros quatro honestos enxergando o que olhos frescos enxergam. Quando os especialistas se enrolam no próprio jargão, ele é a verificação de sanidade.

Quando você gera os conselheiros, force cada um pro extremo do ângulo dele. O equilíbrio é tarefa do presidente. Conselheiro que tenta ser equilibrado sozinho não agrega nada que um único prompt já não daria.

---

## §peer-review

A revisão cruzada é o que separa o conselho de "perguntar 5 vezes e ler". Sem ela, você tem cinco opiniões soltas e nenhuma forma de saber qual confiar. Com ela, os conselheiros se checam — e os pontos cegos que nenhum pegou sozinho aparecem quando todos olham o conjunto.

Regras do passo:

1. **Anonimize sempre.** Mapeie as respostas pra Resposta A–E sorteando a ordem. O revisor não pode saber qual conselheiro escreveu qual resposta. Se souber, vai deferir ao estilo que ele respeita em vez de avaliar o argumento. Guarde o mapa de anonimização — ele entra na transcrição (Passo 6), revelado, mas nunca chega ao revisor.

2. **Três perguntas, sempre as mesmas.** Qual é a mais forte (e por quê), qual tem o maior ponto cego (e qual é), e o que TODAS deixaram passar. A terceira é a que mais rende: é onde emerge o que o conselho inteiro não viu.

3. **Cite por letra.** Força o revisor a apontar evidência concreta, não impressão vaga.

O ouro da revisão cruzada quase sempre está na resposta à pergunta 3 — o ângulo que cinco conselheiros independentes não cobriram, e que só ficou visível olhando o conjunto. Puxe isso com força pra síntese.

---

## §presidência

O presidente não é um sexto conselheiro, e não é um tirador de média. O trabalho dele é destilar, não diluir. Princípios:

- **Convergência independente é sinal forte.** Quando conselheiros que pensam de ângulos opostos chegam no mesmo ponto sem combinar, isso tem peso. Marque como alta confiança.
- **Divergência genuína não se suaviza.** Se o Contrário e o Expansionista batem de frente no preço, não escreva "depende do contexto". Apresente os dois lados, explique a tensão real e tome partido com raciocínio. O usuário quer clareza, não um cobertor.
- **A maioria não manda.** Se 4 de 5 dizem "faz" mas o raciocínio do dissidente é o mais forte, fique com o dissidente. O conselho não é uma votação — é uma deliberação. O melhor argumento ganha, não o mais votado.
- **A recomendação é uma resposta de verdade.** Nunca uma média morna. Nunca "depende". Nunca "considere os dois lados" como veredito. Um veredito que o usuário consegue agir em cima.
- **Critério de pronto.** O presidente diz o que precisa ser verdade no fim pra decisão ter dado certo. Concreto e verificável. Sem isso, ninguém sabe quando parar nem se acertou.
- **Um primeiro passo, não dez.** A última seção é uma única ação concreta. Se você listar dez coisas, o usuário não faz nenhuma. Escolha a que destrava o resto — quase sempre o menor experimento que falsifica a premissa mais arriscada.

---

## §relatório

Gere um arquivo HTML único, autocontido, com CSS inline. Não use framework, não puxe nada de CDN. O relatório do conselho tem cara de **briefing profissional**, não de dashboard escuro — design limpo, claro, sóbrio.

Princípios de design:
- **Fundo claro** (branco ou off-white, #ffffff / #fafafa), tipografia sans-serif legível (system font stack), bordas sutis. Nada espalhafatoso.
- **O veredito do presidente no topo, em destaque**: é o que mais gente lê. As seis seções (concorda / diverge / pontos cegos / recomendação / critério de pronto / primeiro passo) bem separadas e escaneáveis.
- **Visual de concordância × divergência** — um elemento simples mostrando onde os conselheiros se alinharam e onde divergiram. Pode ser um grid, um espectro ou um quadro de posições por conselheiro. Limpo e legível de relance. Use cor de acento suave pra distinguir alinhamento (verde apagado) de conflito (âmbar apagado).
- **Seções recolhíveis por conselheiro** — a resposta completa de cada um dos cinco, colapsada por padrão (`<details>`/`<summary>` nativo, sem JS) pra página não sobrecarregar, mas disponível pra quem quiser cavar. Uma cor de acento suave por conselheiro pra distinguir as seções.
- **Seção recolhível da revisão cruzada** — os destaques do peer review, também colapsada.
- **Rodapé** com timestamp e o que foi levado ao conselho.

Cores de acento sugeridas por conselheiro (suaves, sóbrias):
- O Contrário → vermelho apagado (#c0392b)
- O Pensador de Primeiros Princípios → azul (#2c6fbf)
- O Expansionista → verde (#1e8449)
- O Forasteiro → roxo (#7d3c98)
- O Enxuto → laranja queimado (#b9770e)

Estrutura sugerida do documento:
1. Cabeçalho: "CONSELHO — [o que foi levado ao conselho]" + data
2. A pergunta enquadrada
3. O veredito do presidente (as 6 seções), em destaque
4. Visual de concordância × divergência
5. As 5 respostas dos conselheiros (recolhíveis)
6. Destaques da revisão cruzada (recolhível)
7. Rodapé

Abra o arquivo depois de gerar.
