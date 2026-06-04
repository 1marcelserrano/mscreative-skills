---
name: premortem
description: |
  Roda um premortem sobre qualquer plano, lançamento, produto, contratação,
  pricing, estratégia ou decisão de alto custo de erro. Assume que a decisão
  JÁ FALHOU num horizonte futuro e trabalha de trás pra frente pra achar todo
  motivo que a matou — antes de você gastar dinheiro, tempo ou reputação.
  Método Gary Klein (hindsight prospectivo) + triagem Tigre / Tigre de Papel /
  Elefante + matriz Probabilidade × Impacto + visão de fora (base rates) +
  tripwires datados. Entrega plano revisado, premissa oculta exposta e
  relatório HTML. TRIGGERS: roda um premortem, premortem disso, premortem desse
  plano, faz um premortem, o que pode matar isso, o que pode dar errado, onde
  isso quebra, que ponto cego eu tenho, pré-morte, stress test desse plano,
  testa esse plano, advogado do diabo, devil's advocate, o que estou deixando
  passar, no que não estou pensando, fura esse plano, ataca esse plano, isso
  vai dar certo, me prova que isso falha, premortem de lançamento, premortem de
  contratação, premortem de pricing. Use SEMPRE que houver um plano ou
  compromisso onde errar custa caro e a decisão ainda pode mudar de rumo.
  Acione mesmo sem a palavra "premortem" — basta o usuário pedir pra encontrar
  pontos cegos, furar um plano ou descobrir como algo pode falhar. NÃO dispare
  em pedido de feedback de texto/draft (isso é edição), pergunta factual com
  uma resposta certa, ou decisão já tomada e irreversível.
---

# Premortem

Um postmortem investiga por que algo morreu depois que morreu. O premortem faz o oposto: você imagina que já falhou e descobre por quê antes de começar.

O método é do psicólogo Gary Klein, publicado na Harvard Business Review. Daniel Kahneman — Nobel, autor de "Rápido e Devagar" — chamou de sua técnica de decisão mais valiosa. Google, Goldman Sachs e Procter & Gamble usam antes de decisões grandes.

A intuição central: quando você pergunta "o que pode dar errado?", as pessoas respondem cauteloso, hedge, genérico. Quando você diz "isso já falhou, me conta por quê", o cérebro entra em modo narrativo e gera motivos muito mais específicos, criativos e honestos. Pesquisadores de Wharton e Cornell batizaram isso de "hindsight prospectivo" e mostraram que aumenta de forma significativa a capacidade de identificar causas de resultados futuros.

Por que isso importa numa decisão assistida por IA: o modelo tende ao otimismo cordial. Pergunte "esse plano é bom?" e ele acha razões pra dizer sim. O premortem quebra esse padrão ao forçar o enquadramento "isso está morto, explique como morreu". O modelo para de procurar razões pro plano funcionar e passa a explicar como ele desmoronou.

Esta skill carrega o método canônico completo em `references/metodo-canonico.md` — leia esse arquivo no Passo 2.5 (triagem) e no Passo 5 (relatório), quando precisar dos critérios detalhados e do template HTML.

---

## quando rodar um premortem

Bons alvos:
- Um produto ou feature prestes a ser construído
- Um plano de lançamento com dinheiro ou reputação em jogo
- Uma mudança de pricing ou de modelo de negócio
- Uma contratação prestes a acontecer
- Um pivô de estratégia ou posicionamento
- Uma parceria ou negócio em avaliação
- Qualquer compromisso onde errar custa caro

Maus alvos:
- Ideia vaga sem plano concreto ainda → ajude a planejar primeiro, depois rode o premortem
- Pergunta com uma resposta certa → só responda
- Pedido de feedback num rascunho → isso é edição, não premortem
- Decisão já tomada e irreversível → o premortem só serve enquanto dá pra mudar de rumo

---

## coleta de contexto (a barra mínima)

Um premortem vale o que vale o contexto que recebe. Input vago gera cenário de falha vago que não ajuda ninguém. Antes de rodar, bata uma barra mínima.

### passo 1: varra o contexto que já existe

Antes de perguntar qualquer coisa, procure o que já está disponível:

**A. A conversa atual.** O usuário pode já ter descrito o plano, o lançamento, o produto ou a decisão antes nesta sessão. Releia e extraia o que for relevante.

**B. O workspace.** Varra rápido por arquivos com contexto:
- `CLAUDE.md` (contexto de negócio, preferências, restrições)
- Qualquer pasta `memory/` (perfil de audiência, dados do negócio, decisões passadas)
- Arquivos que o usuário citou ou anexou
- Briefs, planos ou projetos ligados ao que está sendo premortemado

Use `Glob` e `Read` rápidos. Não gaste mais de 30 segundos. Você procura os arquivos-chave que ancoram os cenários de falha na realidade.

### passo 2: avalie se o contexto basta

Depois de varrer, cheque se dá pra rodar um premortem útil. Você precisa de cinco coisas — as três primeiras são obrigatórias, as duas últimas afiam o resultado:

1. **O que é?** — Entendimento claro do que está sendo premortemado. Você precisa descrever de volta em uma frase.
2. **Pra quem / quem é afetado?** — Audiência, cliente, time, stakeholders. Os cenários de falha dependem muito de quem está envolvido.
3. **O que é sucesso?** — Que resultado o usuário espera. A falha se define invertendo o sucesso. Sem saber o que é vencer, você não define o que é perder.
4. **Qual o horizonte de falha?** — Quando a falha ficaria visível. Não fixe "6 meses". Calibre pelo tipo de decisão: lançamento falha em semanas, pricing em um trimestre, contratação em 12-18 meses, estratégia em 1-3 anos. Se o usuário não disser, escolha o horizonte que melhor encaixa e declare a escolha.
5. **Confiança inicial.** — Pergunte: "De 0 a 100%, quanta confiança você tem de que isso dá certo?" Anote o número. No fim, você revisita — o delta torna visível o que o premortem mudou.

### passo 3: preencha as lacunas conversando

Tem os três obrigatórios? Avance pro premortem. Não pergunte o desnecessário.

Falta algum? Pergunte primeiro o mais importante. Uma pergunta por vez. Reavalie depois de cada resposta. Continue até bater a barra, nunca além do necessário. Se der pra inferir do contexto, infira em vez de perguntar.

A meta é bater a barra mínima rápido, sem o usuário sentir que está preenchendo formulário. Conversa, não interrogatório.

---

## como funciona a sessão

### passo 1: monte o enquadramento

Com contexto suficiente, monte o enquadramento explícito. Algo como:

"Tenho contexto suficiente. Vamos rodar o premortem. A premissa: é [data + horizonte calibrado] e [o plano/lançamento/decisão] falhou. Acabou. Estamos olhando pra trás pra entender o que deu errado."

Esse enquadramento é o mecanismo. Ele desloca o modo de "avalie esse plano" (que dispara respostas cordiais) pra "explique por que isso morreu" (que dispara identificação honesta e específica de falha). Sem ele, a análise vira avaliação educada de risco.

### passo 2: gere os motivos de falha (premortem bruto)

**Antes de listar os motivos, rode a aritmética do plano.** Pegue os números que o usuário deu (preço, base, meta, prazo, custo) e faça a conta. Muita falha mora numa contradição entre os próprios números do plano que ninguém somou. Exemplo real: "manter 90% da base" tolera 10% de churn, mas "fechar com receita maior" depois de subir o preço 82% tolera até ~45% de churn — os dois critérios de sucesso colidem, e a meta de retenção morre primeiro. Calcule break-evens, taxas implícitas e onde duas metas se contradizem. Isso vira material pros motivos de falha.

Depois, rode o premortem bruto como uma análise única e abrangente. Sem categorias prescritas, sem lentes, sem amarras. Só o método Klein:

"Este plano falhou em [horizonte]. Gere todo motivo genuíno que pode tê-lo matado. Seja abrangente. Seja específico. Ancore cada motivo nos detalhes reais do plano. Não encha com motivo fraco e não pare cedo se houver mais."

Cada motivo de falha precisa de:
- **Especificidade** — vale pra ESTE plano, não conselho genérico que serve pra qualquer coisa
- **Evidência** — toda razão cita uma evidência (dado, padrão observável, experiência passada). Sem evidência, a razão é ansiedade disfarçada e desce pra Tigre de Papel no Passo 2.5
- **Ameaça real** — não inconveniência menor nem caso extremamente improvável

A lista deve ter o tamanho que for real pro plano. Alguns têm 4 modos de falha genuínos. Outros, 9. Não force número.

### passo 2.5: triagem Tigre / Tigre de Papel / Elefante

Aqui você separa o que merece energia do que só assusta. Leia `references/metodo-canonico.md §triagem` para os critérios completos. Em resumo, classifique cada motivo de falha:

- **Tigre** — ameaça real, com evidência. Cenário de falha plausível e concreto. Ignorar seria negligência. → Vai pro aprofundamento (Passo 3).
- **Tigre de Papel** — assusta no papel, mas é improvável ou de impacto gerenciável quando você olha de perto. Geralmente vem de ansiedade, não de conhecimento específico. → Registra e segue. Não gasta energia.
- **Elefante** — o que todo mundo sabe mas ninguém fala. Costuma ser pessoas, política ou ego, não técnica. É a causa real de falha com mais frequência do que parece. Para um founder ou criador solo, o elefante é a premissa em que ele está emocionalmente investido e se recusa a questionar. → Nomeie explicitamente. Não deixe escapar.

Para cada Tigre, atribua urgência:
- **Bloqueia-Lançamento** — se não resolver, não lança. Precisa de plano de mitigação, dono e data de decisão.
- **Fast-Follow** — resolve nas primeiras 2 semanas pós-lançamento.
- **Monitorar** — acompanha e ataca se escalar.

### passo 3: agentes de aprofundamento (em paralelo)

Pegue cada **Tigre** da triagem e gere um sub-agente por Tigre, todos em paralelo. Mais **um agente red-team da premissa**, separado. Sempre paralelo — sequencial perde tempo e deixa uma resposta contaminar a outra.

**Se você não tem sub-agentes** (ambiente sem essa capacidade, ou você já é um agente que não consegue aninhar): rode cada aprofundamento inline, como passos analíticos distintos e independentes — um por Tigre, mais o red-team. Trate cada um como se fosse um investigador separado: não deixe a análise de um Tigre vazar pra outro. O resultado é o mesmo; só a orquestração muda.

**Template do sub-agente de Tigre:**

```
Você é um investigador num premortem. Recebeu um motivo de falha específico pra analisar a fundo.

O plano:
---
[contexto completo: o que é, pra quem, o que é sucesso, horizonte, + contexto relevante do workspace]
---

ENQUADRAMENTO: É [horizonte]. Este plano falhou.

SEU TIGRE: [o motivo de falha específico, com a urgência atribuída]

Vá fundo nesta falha. Escreva a história de como ela aconteceu de verdade. Seja específico. Use detalhes do plano. Faça parecer real, como estudo de caso de algo que aconteceu mesmo.

Sua saída:

1. A HISTÓRIA DA FALHA: 2-3 parágrafos narrando como essa falha específica se desenrolou. Use detalhes do plano. Nomeie os momentos exatos em que as coisas deram errado e por quê.

2. A PREMISSA SUBJACENTE: A coisa que o usuário tomava como dada e que tornou essa falha possível. Uma frase.

3. SCORE PROBABILIDADE × IMPACTO: Probabilidade (Baixa/Média/Alta) de essa falha acontecer no horizonte + Impacto (Baixo/Médio/Alto) se acontecer. Uma linha de justificativa pra cada.

4. TRIPWIRES: 1-2 gatilhos datados e observáveis — não sensações vagas. Formato: "Se até [data] [métrica/evento observável], então [ação: parar/pivotar/dobrar]." Algo que você consegue medir ou ver.

Máximo 300 palavras. Seja direto. Não suavize. Não enrole.
```

**Template do agente red-team da premissa:**

```
Você é o red-team de um premortem. Seu trabalho não é achar riscos no plano — é atacar a PREMISSA do plano.

O plano:
---
[contexto completo]
---

Pergunte: e se a ideia inteira estiver fundamentalmente errada? Não "tem um risco aqui", mas "a tese central não se sustenta". Ataque a coisa que o usuário nem percebe que está assumindo: que o problema existe, que a audiência se importa, que o timing faz sentido, que ele é a pessoa certa pra isso.

Sua saída (máximo 250 palavras):
1. A PREMISSA QUE NINGUÉM QUESTIONOU: a tese central que, se falsa, derruba tudo.
2. O ARGUMENTO DE QUE ELA É FALSA: o caso mais forte que você consegue montar de que o usuário está errado na raiz.
3. O TESTE MAIS BARATO: o menor experimento que falsificaria essa premissa antes do usuário se comprometer.
```

### passo 4: síntese

Com todos os agentes prontos, leia cada aprofundamento e produza a síntese. Esta é a entrega principal — a maioria lê a síntese e só passa o olho nos cards individuais. Faça específica e acionável.

**RELATÓRIO DO PREMORTEM**

1. **A Falha Mais Provável** — Qual cenário é o mais provável dado o que você sabe? Por quê? É nele que o usuário foca primeiro.

2. **A Falha Mais Perigosa** — Qual causaria mais estrago se acontecesse, mesmo sendo menos provável? É contra essa que vale comprar seguro.

3. **A Matriz Probabilidade × Impacto** — Posicione cada Tigre no grid 2×2 (Prob × Impacto). Os do canto superior-direito (Alta × Alto) são prioridade absoluta. Use os scores dos agentes.

4. **A Premissa Oculta** — De todas as análises, qual a maior premissa que o usuário provavelmente não questionou? Puxe do agente red-team. Costuma ser onde mora o valor real do premortem: o tão óbvio pro usuário que ele esqueceu que era uma premissa.

5. **A Visão de Fora (base rate)** — Saia do plano específico e olhe a classe de referência: "decisões como esta falham em torno de X% das vezes." Se você tem dados, cite. Se não, dê a estimativa honesta com a lógica. Isso ancora a imaginação na taxa histórica real, não no otimismo.

6. **O Plano Revisado** — Que mudanças concretas deixariam o plano mais resistente? Sequencie pelo **menor experimento falsificador primeiro**: a ação mais barata que testa a premissa mais arriscada vem antes de qualquer compromisso grande. Cada revisão mapeia direto pra um cenário de falha. Nada de "considere seu pricing" — diga "rode um piloto de R$X com 20 pessoas antes de travar o preço público de R$Y."

7. **Os Tripwires** — 3-5 gatilhos datados que previnem ou detectam os modos de falha. Cada um: métrica/evento observável + data + ação. Os Tigres que Bloqueiam-Lançamento ganham dono e data de decisão.

8. **Os Elefantes** — Nomeie cada elefante explicitamente. Para cada um, decida: atacar (atribui dono) ou aceitar conscientemente (documenta a aceitação e o porquê). O que não se nomeia, não se resolve.

9. **A Confiança Revisitada** — Lembre a confiança inicial do usuário (passo de contexto). Pergunte de novo agora. O delta mostra o que o premortem mudou. Se caiu muito, ótimo — você evitou um erro caro antes de cometê-lo.

### passo 5: gere o relatório HTML

Gere um relatório HTML visual e salve no workspace do usuário. Leia `references/metodo-canonico.md §relatório` para o template e os princípios de design completos.

**Arquivo:** `premortem-relatorio-[timestamp].html`

Em resumo: arquivo HTML único, CSS inline, fundo escuro, tipografia limpa, escaneável. A síntese no topo (é o que mais gente lê). Um card por modo de falha, com cor por classificação (Tigre / Tigre de Papel / Elefante). O grid da matriz P×I como visual central. Rodapé com timestamp e o que foi premortemado. Abra o arquivo depois de gerar.

### passo 6: salve a transcrição

Salve a transcrição completa como `premortem-transcricao-[timestamp].md`, no mesmo lugar:
- O contexto coletado (o que / pra quem / sucesso / horizonte / confiança inicial)
- Os motivos de falha brutos + a triagem
- Todos os aprofundamentos dos agentes + o red-team
- A síntese completa + a confiança revisitada

---

## formato de saída

Toda sessão produz dois arquivos:

```
premortem-relatorio-[timestamp].html   # relatório visual pra escanear
premortem-transcricao-[timestamp].md    # transcrição completa pra consultar
```

O usuário vê o HTML primeiro. A transcrição fica pra quem quiser entrar no raciocínio de cada cenário.

Dê também um resumo curto no chat: a falha mais provável, a premissa oculta e a única revisão mais importante. Três frases, no máximo. O relatório tem o resto.

---

## exemplo: premortem de um lançamento

**Usuário:** "premortem disso: vou lançar um workshop ao vivo de R$1.500 sobre como usar Claude pra times de marketing. 50 vagas. Alvo: gestores de marketing em empresas de 10-50 pessoas."

**O premortem bruto identifica 6 motivos de falha. A triagem classifica:**

- **Tigre (Bloqueia-Lançamento):** gestor de marketing nessa faixa de empresa precisa de aprovação pra gastar R$1.500 em desenvolvimento — fricção que você não contou. Evidência: ciclo de compra B2B nessa faixa passa por aprovação de orçamento.
- **Tigre (Bloqueia-Lançamento):** quem de fato compra pode ser o solopreneur, não o gestor de time — descasamento entre conteúdo e plateia. Evidência: quem segue conteúdo de IA aplicada hoje é majoritariamente operador solo.
- **Tigre (Fast-Follow):** montar workshop pra times exige ambiente de demo com dados realistas e setup multi-conta — 5 semanas de prep, não as 2 que você orçou.
- **Tigre de Papel:** "um concorrente pode copiar o workshop" — possível, mas o ciclo de execução dele é de meses; baixo impacto agora.
- **Elefante:** você está apaixonado pela tese "gestores de marketing são minha audiência" porque é onde você quer estar, não onde seus compradores estão. Ninguém te disse isso ainda.
- **Tigre de Papel:** "a plataforma de transmissão pode cair" — gerenciável com backup.

**Os agentes vão fundo em cada Tigre + o red-team ataca a premissa "gestores de 10-50 pessoas são alcançáveis".**

**Síntese:** A falha mais provável é o descasamento de audiência — você mira em quem precisa de aprovação pra gastar R$1.500. A mais perigosa: atrair solopreneur em vez de gestor faz seus depoimentos e cases não ressoarem com o comprador-alvo das próximas turmas, o que compõe o problema. A premissa oculta (do red-team): "gestor de marketing em empresa de 10-50 pessoas" não se identifica assim e não frequenta os mesmos lugares — a audiência pode não ser alcançável. Base rate: workshops ao vivo de ticket alto em audiência fria convertem na casa de 1-3%. Plano revisado, menor experimento primeiro: rode um piloto de R$197 pra 20 pessoas. Use pra descobrir se seu comprador real é gestor ou solo, e construa o workshop cheio pra quem de fato aparecer. Tripwire: se em 7 dias de divulgação menos de 10 inscritos forem gestores de time, o alvo está errado — pivota.

---

## notas importantes

- **Sempre gere os agentes de falha em paralelo.** Sequencial perde tempo e deixa respostas anteriores influenciarem as seguintes.
- **Sempre monte o enquadramento explícito.** "Isso já falhou" é o mecanismo psicológico que faz funcionar. Sem ele, a análise vira avaliação educada de risco em vez de identificação honesta de falha.
- **Exija evidência.** Razão de falha sem evidência é ansiedade. Desce pra Tigre de Papel. É isso que separa ameaça real de medo.
- **Abrangente, mas sem encher.** Ache todo motivo genuíno. Não pare em 3 se houver 7. Mas não force 7 se houver 3.
- **A síntese é o produto.** A maioria lê a síntese e passa o olho nos cards. Faça específica e acionável.
- **Não suavize.** O ponto do premortem é te dizer o que você não quer ouvir antes da realidade dizer. Se o plano tem problema sério, diga direto.
- **O plano revisado é concreto.** Nada de "considere testar seu pricing". Diga "rode um piloto de R$197 com 20 pessoas antes de travar o workshop de R$1.500". Toda revisão é algo que dá pra fazer esta semana.
- **Respeite a barra mínima de contexto.** Premortem sobre contexto insuficiente gera falha genérica que desperdiça o tempo do usuário. Melhor uma pergunta a mais do que um premortem ruim.
- **O Elefante é onde mora o ouro.** O que o usuário evita falar costuma ser a causa real. Nomeie mesmo quando for desconfortável.
