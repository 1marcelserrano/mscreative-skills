# Cadeia de prompts — atacar o premortem da mscreative-skills

**Orquestrador:** cadeia sequencial. Cada elo consome o output do anterior, aciona uma skill do repo (dogfooding) e entrega um artefato pronto pra usar. Ordem = prioridade da matriz Probabilidade × Impacto do premortem.

> Como usar: rode os elos em ordem. Onde aparecer `[[COLE O OUTPUT DO ELO ANTERIOR]]`, cole o resultado da etapa anterior antes de enviar. Onde aparecer `Acione a skill X`, garanta que a skill está instalada (ou cole o `SKILL.md` dela no topo da conversa).

---

## Mapa da cadeia

| Elo | Ataca (premortem) | Skill acionada | Consome | Entrega |
|---|---|---|---|---|
| 1 · Foco | #4 Foco difuso (Elefante) | `llm-council` | síntese do premortem | Doc "Foco 90 dias": 1 objetivo primário + métrica-norte |
| 2 · Experimento | #1 Descoberta · #3 Mercado PT-BR | `nem-parece-ia` | Foco 90 dias | Roteiro de 1 peça (1 skill rodando) + CTA rastreável + critério de 14 dias |
| 3 · Motor de conteúdo | #1 Descoberta (contínuo) | `geo-content-brief` + `nem-parece-ia` | resultado do experimento | Calendário de 2 semanas + brief GEO por peça |
| 4 · Funil | #2 Funil sem captura | `nem-parece-ia` | Foco 90 dias + canal | CTA do README + rodapé dos HTMLs + 3 e-mails de boas-vindas |
| 5 · Ativação | #5 Ativação · #8 Qualidade desigual · meta-elefante | `nem-parece-ia` | skill-vitrine | Template de README com output no topo + ordem de vitrine + decisão references |
| 6 · Robustez | #6 Drift | — (técnico) | estrutura dos SKILL.md | GitHub Action que valida frontmatter + caminhos |
| 7 · Licença | #7 Commons Clause | `llm-council` | Foco 90 dias | Decisão documentada + cabeçalho LICENSE/NOTICE |
| 8 · Por skill | os 6 premortems individuais | a própria skill de cada caso | tudo acima | 1 edição concreta por skill |
| 9 · Fechar o loop | todos (verificação) | `premortem` | artefatos dos elos 1–8 | Painel de tripwires 30/60/90 + gatilho de re-premortem |

---

## ELO 1 — A Decisão de Foco  ·  ataca #4 (Elefante: 4 metas em conflito)

```
Acione a skill llm-council.

Decisão a julgar: pelos próximos 90 dias, qual destes quatro deve ser o objetivo
PRIMÁRIO da coleção mscreative-skills (os outros três viram efeitos de segunda
ordem, não metas paralelas)?
  A) adoção real     B) tração open-source     C) distribuição de marca     D) monetização indireta

Contexto (do premortem):
- O premortem apontou que perseguir os quatro ao mesmo tempo, solo, em 3-6 meses,
  dispersa o foco e entrega nenhum. Atrito mínimo (bom pra adoção/tração) colide
  com ponto de captura (necessário pra monetização).
- O elefante nomeado: o autor não quer escolher.

Quero do conselho:
1. O veredito: UM objetivo primário, com o argumento mais forte.
2. Quais dos outros três ele puxa de graça (efeitos de segunda ordem) e qual ele
   sacrifica conscientemente.
3. A MÉTRICA-NORTE única que mede esse objetivo em 90 dias (um número que sobe).
4. O primeiro passo desta semana.

Entregue como um doc de 1 página chamado "FOCO 90 DIAS" — é o input de todos os
próximos prompts da cadeia.
```

---

## ELO 2 — O Menor Experimento de Distribuição  ·  ataca #1 (Descoberta) + #3 (Mercado PT-BR)

```
[[COLE AQUI O DOC "FOCO 90 DIAS" DO ELO 1]]

Papel: você é meu estrategista de distribuição. O premortem disse que a falha mais
provável é "descoberta zero" e que a premissa a falsificar é "qualidade basta".
Vamos desenhar o menor experimento (~R$0) que testa isso em 14 dias.

1. Escolha UMA skill-vitrine (a mais forte e mais demonstrável: premortem ou
   nem-parece-ia). Justifique em 1 linha à luz do FOCO 90 DIAS.
2. Defina 1 caso real e concreto onde essa skill brilha em 60-90 segundos.
3. Escreva o ROTEIRO da peça (fio/vídeo curto) mostrando a skill rodando nesse caso:
   gancho nos primeiros 3 segundos, o "antes", a skill rodando, o "depois", e UM CTA
   único e rastreável (link com UTM ou link encurtado dedicado).
4. Escolha o canal onde minha audiência PT-BR realmente está (não o GitHub).
5. Defina o tripwire: "Se em 14 dias o CTA tiver menos de [N] cliques rastreáveis,
   o gargalo é canal/oferta, não produto."

Depois de escrever o roteiro, acione a skill nem-parece-ia para revisar a copy do
roteiro e do CTA — quero que não soe IA nem marketing genérico.

Entregue: o roteiro final + o plano de publicação (canal, data, métrica, tripwire).
```

---

## ELO 3 — O Motor de Conteúdo / Descoberta  ·  ataca #1 (Descoberta, contínuo)

```
[[COLE AQUI O ROTEIRO + PLANO DO ELO 2]]

Um experimento não é um motor. Transforme a peça única acima numa cadência de 2
semanas que cubra a coleção sem me esgotar.

1. Monte um calendário de 2 semanas: uma peça por skill-vitrine (comece pelas 2 mais
   fortes), com formato, gancho e CTA de cada uma. Reaproveite o padrão do ELO 2.
2. Para cada peça que vira também um artigo/página (não só fio social), acione a skill
   geo-content-brief no modo Estratégia: gere o brief de 8 campos pra essa página ser
   achável no Google E citável por AI Overviews/ChatGPT/Perplexity. (Ataca o mercado
   PT-BR pequeno ampliando a superfície de descoberta para além do GitHub.)
3. Para cada peça social, passe a copy pela skill nem-parece-ia antes de publicar.

Entregue: o calendário de 2 semanas (tabela: dia / skill / formato / gancho / CTA /
brief GEO se aplicável), pronto pra executar.
```

---

## ELO 4 — O Ponto de Captura / Funil  ·  ataca #2 (Funil sem captura)

```
[[COLE AQUI O FOCO 90 DIAS + O CANAL DEFINIDO NO ELO 2]]

O premortem disse que a falha mais perigosa é o funil sem nenhum ponto de captura:
as skills rodam local, geram HTML local, e nada volta pro MSCREATIVE. Vamos consertar
a aritmética do funil — sem matar a adoção com atrito.

Produza 3 artefatos prontos:

1. BLOCO DE CAPTURA PRO TOPO DO README — 2-3 linhas + 1 link único (newsletter/lista),
   posicionado pra ser visto sem virar muro. Foco em valor ("receba a próxima skill +
   1 caso de uso por semana"), não em "assine".

2. RODAPÉ PADRÃO PROS HTMLs GERADOS PELAS SKILLS — um snippet HTML curto, discreto, que
   cada skill (premortem, llm-council, etc.) injeta no rodapé do relatório que gera, com
   1 link rastreável de volta. É o único ponto onde o uso vira relacionamento — desenhe
   pra ser útil, não intrusivo.

3. SEQUÊNCIA DE 3 E-MAILS DE BOAS-VINDAS — pra quem entra pela captura: (e1) entrega de
   valor imediato, (e2) caso de uso de uma skill, (e3) a ponte pro próximo passo alinhado
   ao FOCO 90 DIAS (se monetização é segunda ordem, a ponte é suave).

Acione a skill nem-parece-ia em toda a copy antes de finalizar.
Entregue os 3 artefatos prontos pra colar.
```

---

## ELO 5 — Ativação: ver antes de instalar  ·  ataca #5 (Ativação) + #8 (Qualidade desigual) + meta-elefante (references não viajam)

```
[[COLE AQUI A SKILL-VITRINE ESCOLHIDA NO ELO 2]]

O premortem apontou: (a) ativação fraca — o estranho lê a promessa, não vê o resultado,
e cola 273-311 linhas num chat; (b) qualidade desigual entre skills dilui a marca;
(c) meta-elefante — as references não viajam no caminho de instalação de menor atrito.

Produza:

1. TEMPLATE DE README POR SKILL com o output de exemplo (GIF ou bloco de resultado) no
   TOPO, antes da explicação — "veja antes de instalar". Defina exatamente o que mostrar
   pra cada uma das 6 skills.

2. ORDEM DE VITRINE no README principal: lidere com as 2 skills mais completas (premortem
   + nem-parece-ia) como porta de entrada; sequencie o resto. Justifique a ordem.

3. DECISÃO SOBRE AS REFERENCES: para cada skill que depende de references/ (premortem,
   llm-council, nem-parece-ia, cowork-setup), decida entre (i) embutir o essencial inline
   no SKILL.md ou (ii) tornar o caminho completo o default explícito. Recomende por skill
   e escreva o aviso que vai no topo de cada SKILL.md.

Acione a skill nem-parece-ia nos textos de README.
Entregue os 3 artefatos prontos.
```

---

## ELO 6 — Robustez: CI anti-drift  ·  ataca #6 (Drift)

```
[[COLE AQUI A ESTRUTURA DE UM SKILL.md DO REPO — frontmatter + cabeçalhos]]

O premortem apontou risco de drift: o formato de skills do Claude é novo e muda; sem
validação automatizada, as instruções de instalação quebram em silêncio.

Crie um GitHub Action (.github/workflows/validate-skills.yml) que, a cada push e PR:
1. Valida que todo skills/*/SKILL.md tem frontmatter YAML bem-formado com os campos
   obrigatórios (name, description).
2. Confere que o `name` do frontmatter bate com o nome da pasta.
3. Verifica que os caminhos de instalação citados no README (ex: ~/.claude/skills/$SKILL,
   a URL raw do curl) existem/estão consistentes com a estrutura do repo.
4. Falha o check com mensagem clara apontando o arquivo e o problema.

Entregue: o YAML do workflow completo + qualquer script auxiliar (ex: um validador em
Python/Node), prontos pra commitar.
```

---

## ELO 7 — Licença e posicionamento OSS  ·  ataca #7 (Commons Clause)

```
[[COLE AQUI O FOCO 90 DIAS DO ELO 1]]

Acione a skill llm-council.

Decisão: a coleção usa MIT + Commons Clause (não é OSI-approved). O premortem classificou
isso como Tigre de Papel — atrita tração OSS e pode ser barrado de awesome-lists, mas o
impacto é baixo frente ao gargalo de descoberta. A decisão depende do objetivo primário
escolhido no FOCO 90 DIAS.

Pergunta ao conselho: mantenho MIT + Commons Clause, ou migro pra MIT puro?
- Se "tração OSS" for o objetivo primário, o peso pende pra MIT puro.
- Se "monetização/marca" for primário, a Commons Clause protege contra reempacotamento pago.

Quero: o veredito + a justificativa + o cabeçalho final do LICENSE e da NOTICE já escrito
pra refletir a decisão (incluindo, se mantiver a Commons Clause, 1 parágrafo no topo
explicando o porquê em linguagem humana, pra reduzir a fricção de quem lê).
```

---

## ELO 8 — Premortem por skill: os 6 fixes  ·  ataca os 6 premortems individuais

> Rode um sub-prompt por skill. Cada um aciona a própria skill em questão e entrega 1 edição concreta.

**8.1 · premortem** (falha: 273 linhas + dependência de sub-agentes paralelos)
```
Leia o SKILL.md da skill premortem. O premortem dela apontou: é longa demais pra colar
(estoura/dilui contexto) e o método pede sub-agentes paralelos que claude.ai/ChatGPT não
têm. Entregue: (a) uma versão enxuta do bloco de coleta de contexto que reduz o atrito
sem perder a barra mínima; (b) um aviso claro no topo sobre o fallback inline quando não
há sub-agentes. Mostre o diff pronto pra aplicar.
```

**8.2 · llm-council** (falha: 5 vozes do mesmo modelo = correlação, não diversidade)
```
Leia o SKILL.md da skill llm-council. O premortem apontou: simular 5 conselheiros num
único modelo gera correlação, não diversidade real. Entregue: uma revisão do prompt dos
conselheiros que força premissas/papéis MAIS ortogonais (cada um com um eixo de discordância
explícito e proibido de concordar de saída), reduzindo a convergência precoce. Diff pronto.
```

**8.3 · oracle-diagnostic-lite** (falha: só diagnostica, frustra quem quer a saída)
```
Leia o SKILL.md da skill oracle-diagnostic-lite. O premortem apontou: por design ela não
prescreve, e isso frustra quem quer a solução; é o funil perfeito pra oferta paga, mas sem
CTA vira frustração. Entregue: o texto de fechamento da skill com um CTA explícito e honesto
("isto é a leitura de superfície; a consulta completa é →") que respeita o contrato da skill
sem prometer demais. Diff pronto.
```

**8.4 · nem-parece-ia** (falha: references PT-BR não viajam no caminho 1)
```
Leia o SKILL.md da skill nem-parece-ia e a lista de arquivos em references/. O premortem
apontou: a diferenciação está nas references, que não viajam quando se copia só o SKILL.md —
e essa é a skill que mais se expõe ao falhar. Entregue: o conjunto mínimo das references que
precisa ser embutido inline no SKILL.md pra a skill entregar valor real sozinha. Mostre o
trecho consolidado pronto pra inserir.
```

**8.5 · geo-content-brief** (falha: conselho perecível num campo volátil)
```
Leia o SKILL.md da skill geo-content-brief. O premortem apontou: GEO/AEO muda mensalmente e
a skill cita dados de 2025-2026 — risco de envelhecer mal com ar de autoridade. Entregue:
(a) um bloco de "validade e calibração" pro topo da skill ("calibrado em jun/2026 — revise as
faixas de citação a cada trimestre"); (b) a lista dos 3-4 números/heurísticas mais perecíveis
que devem ser revisados. Diff pronto.
```

**8.6 · cowork-setup** (falha: acoplada a um produto que muda)
```
Leia o SKILL.md da skill cowork-setup. O premortem apontou: é a mais acoplada à estrutura do
Claude Cowork, que muda (já foi v1→v3). Entregue: (a) a lista de pontos de acoplamento (caminhos,
nomes de arquivo, estrutura de workspace) que devem ser checados pelo CI do ELO 6; (b) uma nota
de versão no topo que declara contra qual versão do Cowork ela foi validada. Diff pronto.
```

---

## ELO 9 — Fechar o loop: tripwires + re-premortem  ·  verificação de todos os pontos

```
[[COLE AQUI OS ARTEFATOS-CHAVE DOS ELOS 1 A 8 — ou um resumo de 1 linha de cada]]

Acione a skill premortem em modo leve, só pra fechar o loop.

Com base no que foi de fato produzido na cadeia, monte o PAINEL DE TRIPWIRES:
- 30 dias: descoberta — métrica do ELO 2/3 + piso + ação.
- 60 dias: ativação — caso de uso de terceiro documentado + ação.
- 90 dias: funil/foco — métrica-norte do FOCO 90 DIAS + piso + ação.
Cada tripwire no formato: "Se até [data] [métrica] [limiar], então [parar/pivotar/dobrar]."

E defina o gatilho de RE-PREMORTEM: a condição em que vale rodar o premortem de novo
(ex: ao bater/furar 2 dos 3 tripwires, ou antes de lançar uma oferta paga).

Entregue o painel pronto pra colar num doc de acompanhamento.
```

---

*Cadeia desenhada a partir do premortem de 12/06/2026. Orquestração sequencial, dogfooding das skills do repo, cada elo entrega artefato pronto.*
