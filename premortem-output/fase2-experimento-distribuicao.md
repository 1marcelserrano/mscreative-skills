# FASE 2 — O Menor Experimento de Distribuição

**Decidido em:** 12/06/2026 · cadeia orquestrada · serve ao FOCO 90 DIAS (adoção real)

## Decisões desta fase

| Decisão | Escolha |
|---|---|
| **Skill-vitrine** | `nem-parece-ia` (recomendação do orquestrador, dado o canal) |
| **Canal** | Substack (base própria + captura embutida) espelhado no Instagram (alcance) |
| **Tripwire (14 dias)** | menos de **15 cliques rastreáveis** no link do repo → tese "qualidade basta" não se sustenta no canal |
| **Caso real** | reescrita de um texto com cara de IA, ao vivo, com o antes/depois exposto |

> Por que `nem-parece-ia`: o público de Substack escreve e lê — o antes/depois de um texto é legível em 5 segundos, não exige explicar "o que é uma skill", e espelha direto num carrossel. Ângulo meta: a peça de lançamento da skill que tira a cara de IA precisa, ela mesma, não soar como IA.

> Por que o canal é forte: **o Substack é o ponto de captura.** Cada leitor que assina vira e-mail na lista (a métrica-guarda do FOCO 90 DIAS) sem você construir funil à parte. O Instagram puxa gente fria; o Substack captura e retém.

---

## A peça — Substack (base)

**Formato:** post curto-médio (500-700 palavras), com o antes/depois embutido. Tempo de leitura ~3 min.

**Título (3 opções, escolha 1):**
1. *"Escrevi este parágrafo com IA. Você consegue dizer onde ele te perde?"*
2. *"O problema não é a IA escrever por você. É ela escrever igual a todo mundo."*
3. *"Peguei um texto 'profissional' e tirei a cara de robô. O diff embaixo."*

**Estrutura:**

1. **Gancho (primeiras 2 linhas — é o que aparece no preview do e-mail):**
   > Todo texto de IA tem o mesmo cheiro: abertura vazia, três adjetivos onde cabia um, aquele "não se trata apenas de X, mas de Y". Você sente antes de saber por quê.

2. **O antes (cole um texto real com cara de IA — 1 parágrafo):**
   Um trecho genérico, inflado, do tipo que sai de qualquer chat. Curto. Real.

3. **O diagnóstico (2-3 frases):**
   Nomeie os vícios — abertura performática, sujeito abstrato, contraste de espelho, ritmo robótico. Mostre que tem método, não é "achismo".

4. **O depois (o mesmo texto, revisado):**
   A versão que soa humana. O contraste faz o trabalho — não precisa vender, só mostrar.

5. **A virada (o "como"):**
   > Isto não fui eu reescrevendo no olho. É uma skill — um conjunto de instruções que o Claude segue — que eu abri de graça. Você cola, manda seu texto, e ela faz esse diagnóstico e essa revisão. Em português, calibrada pro português.

6. **CTA duplo:**
   - *Assinar* (implícito no Substack — convide: "se você escreve e não quer soar como máquina, assina; toda semana eu solto uma dessas").
   - *Instalar/ver a skill:* **[link rastreável com UTM]** → repo no GitHub.

---

## O espelho — Instagram

**Formato:** carrossel (mais simples que Reel pra estrear) OU Reel de 60-90s. Comece pelo carrossel.

**Carrossel (6 telas):**
1. **Capa/gancho:** "Todo texto de IA tem o mesmo cheiro." + subtítulo: "consegue dizer qual destes foi a máquina?"
2. **O antes:** o parágrafo com cara de IA, destacado.
3. **Os vícios:** 3-4 setas apontando abertura vazia / contraste performático / sujeito abstrato / ritmo robótico.
4. **O depois:** a versão revisada, lado a lado.
5. **A virada:** "Isto é uma skill grátis pro Claude. Em português."
6. **CTA:** "Link na bio → instala em 2 minutos." (bio aponta pro Substack, que aponta pro repo com UTM.)

**Reel (se preferir vídeo):** mesma sequência, você narrando por cima do texto na tela. Gancho nos 3 primeiros segundos: leia o "antes" em voz alta e diga "sente o cheiro?".

---

## O rastreamento (sem isso, o experimento não existe)

- **Link único com UTM** pro repo, ex.:
  `https://github.com/1marcelserrano/mscreative-skills?utm_source=substack&utm_medium=post&utm_campaign=nemparece-01`
  (e uma variante `utm_source=instagram` pro espelho — pra saber qual canal puxa.)
- Use um encurtador que conta cliques (Dub, Bitly, ou o próprio painel do Substack pra links).
- **Captura = assinantes do Substack.** Anote o nº de assinantes antes de publicar pra medir o delta.

## A métrica de 14 dias

| O que medir | Onde | Piso (tripwire) |
|---|---|---|
| Cliques rastreáveis no link do repo | encurtador / UTM | **15** |
| Novos assinantes do Substack (captura) | painel Substack | acompanhar (sem piso ainda) |
| Instalações reais (curl/clone) | difícil medir direto — proxy = cliques + menções | — |

## O tripwire (decidido a frio, agora)

> **Se até [data = hoje + 14 dias] o link do repo tiver menos de 15 cliques rastreáveis**, a tese
> "qualidade gera adoção" não se sustenta neste canal → o gargalo é distribuição/canal, não produto:
> antes de produzir qualquer peça nova, repensar canal e gancho (não a skill).

## Definição de pronto desta fase

A Fase 2 vira **Concluído** quando a peça foi publicada nos dois canais, o link rastreável está no ar, e o nº de assinantes-base foi anotado. A leitura do resultado (14 dias depois) alimenta a Fase 3 (motor de conteúdo) ou dispara o tripwire.

---

*Artefato da Fase 2. A copy acima deve passar pela própria `nem-parece-ia` antes de publicar — a peça precisa praticar o que prega. A IA orquestra e prepara; o usuário decide e publica.*
