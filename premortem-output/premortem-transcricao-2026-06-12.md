# Premortem — mscreative-skills (transcrição completa)

**Data:** 12/06/2026
**Alvo:** o repositório `mscreative-skills` (a coleção como um todo) + cada uma das 6 sub-skills
**Método:** Gary Klein (hindsight prospectivo) + triagem Tigre / Tigre de Papel / Elefante + matriz Probabilidade × Impacto + visão de fora (base rates) + tripwires datados.

---

## 1. Contexto coletado (a barra mínima)

| Dimensão | Resposta |
|---|---|
| **O que é?** | Coleção pública e curada de 6 skills PT-BR de decisão para o Claude (Claude Code, Cowork, claude.ai): `premortem`, `llm-council`, `oracle-diagnostic-lite`, `nem-parece-ia`, `geo-content-brief`, `cowork-setup`. Open source sob MIT + Commons Clause. Distribuição por copiar/colar, `curl` ou `git clone`. Autor: MSCREATIVE.SYSTEMS™ (Barcelona). |
| **Pra quem?** | Usuários PT-BR avançados de Claude — founders, criadores, profissionais de marketing. Nicho dentro de um ecossistema de descoberta majoritariamente anglófono. |
| **O que é sucesso?** | **Quatro frentes simultâneas** (confirmado pelo usuário): (a) **adoção real** — gente instala e usa no dia a dia; (b) **tração open-source** — stars/forks/menções; (c) **distribuição de marca** — autoridade e leads pro MSCREATIVE; (d) **monetização indireta** — funil pra uma oferta paga. |
| **Horizonte de falha** | **3–6 meses** (confirmado) — janela típica de momentum de OSS. |
| **Confiança inicial** | Não capturada em número. A recalibração fica como exercício final pro autor. |

### Enquadramento

> É dezembro de 2026. A coleção `mscreative-skills` falhou em todas as quatro frentes — ninguém adota de verdade, não pegou tração, não virou distribuição de marca e não gerou um único lead pago. O repo está parado. Estamos olhando pra trás pra entender o que a matou.

---

## 2. Aritmética do plano (antes dos motivos)

- **3 caminhos de instalação.** O caminho 1 (copiar o `SKILL.md`) é o de menor atrito — e o mais usado — mas **não deixa rastro mensurável** (não dá pra medir adoção) e **não carrega a pasta `references/`**, entregando a versão degradada das skills mais ricas.
- **Zero pontos de captura no funil.** Não há e-mail, CTA ou link de volta pro MSCREATIVE dentro do output das skills nem no corpo do README — só um rodapé "Forjado na MSCREATIVE.SYSTEMS". Para o objetivo "monetização indireta", o funil tem **zero entradas** → conversão matematicamente ~0.
- **Tamanho dos SKILL.md** (atrito de ativação no caminho 1):
  - `llm-council` — 311 linhas
  - `premortem` — 273 linhas
  - `geo-content-brief` — 186 linhas
  - `nem-parece-ia` — 116 linhas
  - `cowork-setup` — 110 linhas
  - `oracle-diagnostic-lite` — 90 linhas
  Colar 300+ linhas num chat dilui o contexto do pedido ou estoura a janela.
- **Conflito entre os quatro objetivos.** Atrito mínimo (bom pra adoção/tração) ⟂ ponto de captura/gate (necessário pra monetização). Os critérios de sucesso colidem; otimizar um penaliza outro.
- **Descoberta.** Nenhum canal de distribuição declarado. OSS não se distribui sozinho.

---

## 3. Premortem bruto — motivos de falha (repo inteiro)

1. **Descoberta zero / "build it and they will come".** Publicar ≠ distribuir. Sem motor de distribuição, 6 skills PT-BR ficam invisíveis. *Evidência:* a maioria dos repos de prompts/skills morre com <10 stars; descoberta é o gargalo nº1 de OSS.
2. **Funil de monetização sem ponto de captura.** As skills rodam local, geram HTML local, e nada volta pro MSCREATIVE. *Evidência:* aritmética — zero entradas no funil.
3. **Mercado-alvo estruturalmente pequeno (PT-BR no GitHub global).** Awesome-lists e discovery são anglófonos; Cowork é novo e pequeno. *Evidência:* penetração de Claude Code/Cowork concentrada em dev anglófono.
4. **Quatro objetivos em conflito dispersam o foco.** Querer adoção + tração + marca + monetização ao mesmo tempo, solo, em 3–6 meses, entrega nenhum. *Evidência:* foco difuso é causa clássica de morte de projeto solo. **(também Elefante)**
5. **Ativação fraca — sem prova de valor antes de instalar.** Sem GIF/exemplo rodável; caminho 1 cola 273–311 linhas. *Evidência:* tamanho dos SKILL.md + ausência de output de exemplo no README.
6. **Drift / apodrecimento.** Formato de skills do Claude é novo e muda; sem CI de validação, instruções quebram silenciosamente. *Evidência:* `cowork-setup` já foi v1→v3 por mudança de produto.
7. **Licença Commons Clause atrita adoção/tração.** Não é OSI-approved; algumas listas exigem OSI. *Evidência:* Commons Clause é conhecido por gerar fricção e ser barrado de listas.
8. **Qualidade desigual entre skills dilui a marca.** Profundidade varia (references ricas vs. skills finas). *Evidência:* primeira impressão dominada pelo pior ponto de contato.

---

## 4. Triagem Tigre / Tigre de Papel / Elefante

| # | Motivo | Classe | Urgência | Prob × Impacto |
|---|---|---|---|---|
| 1 | Descoberta zero | **Tigre** | Bloqueia-Lançamento | Alta × Alto |
| 2 | Funil sem captura | **Tigre** | Bloqueia-Lançamento | Alta × Alto |
| 3 | Mercado PT-BR pequeno | **Tigre** | Monitorar | Média × Alto |
| 4 | Foco difuso (4 metas) | **Tigre + Elefante** | Bloqueia-Lançamento | Alta × Alto |
| 5 | Ativação fraca | **Tigre** | Fast-Follow | Alta × Médio |
| 6 | Drift / manutenção | **Tigre** | Monitorar | Média × Médio |
| 7 | Licença Commons Clause | **Tigre de Papel** | Monitorar | Baixa × Baixo |
| 8 | Qualidade desigual | **Tigre de Papel** | Monitorar | Média × Baixo |

---

## 5. Aprofundamentos (um por Tigre)

### Tigre #1 — Descoberta zero
- **História:** repo publicado, anunciado uma vez, deixado esperando. Sem fios/conteúdo, sem presença nas listas onde devs procuram skills, sem cadência. Em 3 meses o tráfego orgânico vira ruído. A qualidade nunca foi o problema — as skills nunca foram vistas.
- **Premissa:** publicar é distribuir. (É só tornar disponível.)
- **Prob × Impacto:** Alta × Alto — destino default de OSS sem canal.
- **Tripwire:** 30 dias após o 1º conteúdo de distribuição sem passar de um piso de cliques rastreáveis → o gargalo é canal; pare de construir, distribua.

### Tigre #2 — Funil sem captura
- **História:** skills até usadas, cada execução gerou um HTML lindo na máquina do usuário com um rodapé que ninguém clica. Nenhum e-mail, nenhuma lista, nenhum CTA. Na hora de monetizar, não havia ninguém pra quem falar — o uso aconteceu e evaporou.
- **Premissa:** uso gratuito vira relacionamento monetizável por osmose. (Não vira sem captura.)
- **Prob × Impacto:** Alta × Alto — determinístico.
- **Tripwire:** 90 dias com captura de e-mail abaixo de um piso → monetização indireta não fecha nesse formato; aceite brand-play ou redesenhe.

### Tigre #3 — Mercado PT-BR pequeno
- **História:** skills competiram por descoberta num ecossistema anglófono; teto de alcance orgânico bateu cedo, por restrição de mercado, não por qualidade.
- **Premissa:** o mercado PT-BR de usuários avançados de Claude é grande o bastante pros quatro objetivos.
- **Prob × Impacto:** Média × Alto — restrição estrutural; contorna-se com canal próprio, não se "conserta".
- **Tripwire:** se a tração depender 100% de descoberta orgânica no GitHub, não virá — PT-BR exige canal próprio.

### Tigre/Elefante #4 — Foco difuso
- **História:** os quatro objetivos puxaram pra direções opostas; cada decisão de produto teve quatro donos e nenhum vencedor. Atrito mínimo (tração) matou captura (monetização) e vice-versa.
- **Premissa (elefante):** dá pra perseguir os quatro de uma vez — porque escolher um dói. O não-dito: o autor não quer escolher.
- **Prob × Impacto:** Alta × Alto.
- **Decisão:** **atacar** — 1 objetivo primário por 90 dias (recomendo distribuição+adoção), os outros três rebaixados a efeitos de segunda ordem. Documentar.

### Tigre #5 — Ativação fraca
- **História:** o estranho leu a promessa, não viu o resultado; pra testar pelo caminho fácil colou 273–311 linhas num chat; rodou uma vez, o output não gritou valor, não voltou. Sem "veja antes de instalar", a ativação despencou — nas skills que carregam a marca.
- **Premissa:** o usuário paga o custo de ativação antes de ver a prova.
- **Prob × Impacto:** Alta × Médio — composta com a descoberta.
- **Tripwire:** 60 dias sem um caso de uso de terceiro documentado → ativação quebrada; adicione exemplos rodáveis antes de nova skill.

### Tigre #6 — Drift
- **História:** um ajuste no frontmatter, no trigger ou no caminho `~/.claude/skills` quebrou a instalação e as skills pararam de disparar. Sem CI, o drift foi silencioso até a issue "não funciona mais".
- **Premissa:** formato/caminhos do Claude/Cowork são estáveis no horizonte. (São de tudo, menos.)
- **Prob × Impacto:** Média × Médio — inevitável no tempo, gerenciável com validação.
- **Tripwire:** CI que valida frontmatter + caminhos a cada push.

---

## 6. Red-team da premissa

- **A premissa que ninguém questionou:** *"Skills excelentes se distribuem sozinhas — a qualidade é o gargalo."*
- **O argumento de que é falsa:** o autor investiu pesado em qualidade e acertou — as skills são boas. Mas nenhum dos quatro objetivos é limitado por qualidade. Adoção é limitada por descoberta+ativação; tração por canal; marca por distribuição; monetização por captura. A tese "faço skills excelentes em PT-BR ⇒ os quatro vêm" confunde condição necessária com suficiente. Qualidade é o ingresso, não o motor.
- **O teste mais barato (falsificador):** pegue UMA skill (premortem ou nem-parece-ia), grave 1 vídeo/fio de um caso real rodando, publique onde sua audiência PT-BR está, com UM CTA rastreável. Meça cliques/instalações em 14 dias. Se um conteúdo bem-feito de uma skill ótima não move nada, o problema não é o repo — é canal/oferta, e nenhuma skill nova resolve.

---

## 7. Síntese (relatório)

1. **Falha mais provável:** descoberta zero — as skills são boas e ninguém as vê.
2. **Falha mais perigosa:** funil sem ponto de captura — impossibilita monetização por construção e mascara o problema como "construção de audiência".
3. **Matriz P×I:** canto Alta×Alto = #1 descoberta, #2 funil, #4 foco difuso → prioridade absoluta.
4. **Premissa oculta:** "qualidade é o gargalo" — é distribuição e funil.
5. **Base rate:** ~5–10% dos repos de skills/prompts pegam tração; conversão OSS→pago sem captura ~0%. (Estimativas grosseiras; a direção é o ponto.)
6. **Plano revisado (menor experimento primeiro):**
   - (a) Escolher 1 objetivo primário por 90 dias — distribuição + adoção; largar stars como vaidade.
   - (b) **Menor experimento (~R$0):** 1 vídeo/fio de 1 skill rodando, 1 CTA rastreável, medir em 14 dias.
   - (c) Adicionar ponto de captura: link no topo do README + rodapé do HTML gerado ("feito com mscreative-skills — receba as próximas em [newsletter]").
   - (d) GIF de output no topo do README de cada skill.
   - (e) CI mínimo validando frontmatter YAML + caminhos de instalação.
   - (f) Liderar o README com premortem + nem-parece-ia (vitrine das mais fortes).
   - (g) Decidir a licença em função do objetivo primário (MIT puro se tração OSS; senão documentar a Commons Clause).
   - (h) Para skills que dependem de `references/`, embutir o essencial inline ou forçar o caminho completo.
7. **Tripwires:** ver §5 — 30/60/90 dias para descoberta, ativação e captura.
8. **Elefantes:**
   - *Repo:* o autor quer "vitrine de marca" mas evita o trabalho de distribuição/funil — onde os quatro objetivos moram. Construir mais skills é fuga produtiva. **Atacar.**
   - *Sub-skills (meta-elefante):* as skills mais valiosas dependem de `references/` que não viajam no caminho de menor atrito. Defeito de distribuição que mina a qualidade percebida nas skills da marca. **Atacar.**
9. **Confiança revisitada:** re-pergunte agora — *de 0 a 100%, quanta confiança de que isto bate os quatro objetivos em 6 meses?* Se caiu, ótimo: o buraco de distribuição/funil ficou visível antes de mais 6 meses de construção.

---

## 8. Premortem por sub-skill

### premortem (v1.0) — Tigre
- **Falha:** 273 linhas coladas no caminho 1 estouram/diluem contexto; método pede sub-agentes paralelos que claude.ai/ChatGPT/Gemini não têm (fallback inline dilui).
- **Premissa oculta:** o usuário traz contexto suficiente — a maioria traz plano vago.
- **Tripwire:** se >50% das rodagens travam na coleta de contexto, a barra mínima está alta demais.

### llm-council (v1.0) — Tigre
- **Falha:** simular 5 conselheiros + revisão cruzada num único modelo é caro e lento; sem multi-modelo real é o mesmo modelo fingindo 5 vozes → mina "diversidade de ângulos". Maior SKILL.md (311 linhas).
- **Premissa oculta:** 5 vozes do mesmo modelo dão diversidade real (geram correlação).
- **Tripwire:** se os conselheiros convergem cedo, a diversidade é teatral — force papéis mais ortogonais.

### oracle-diagnostic-lite (v1.0) — Tigre
- **Falha:** por design não prescreve solução; quem quer a saída fica frustrado ("e agora?"). A contenção que a mantém honesta gera não-retorno.
- **Premissa oculta:** o usuário aceita o contrato "só diagnóstico". É o funil perfeito pra oferta paga, mas sem CTA vira frustração.
- **Tripwire:** é a skill que mais pede um CTA explícito; sem ele, trabalha contra a monetização.

### nem-parece-ia (v1.0) — Tigre
- **Falha:** maior risco de "uncanny valley" — promete remover cara de IA e, se falhar, a falha é auto-evidente e embaraçosa. Mais commoditizada; a diferenciação está nas `references/` PT-BR que não viajam no caminho 1.
- **Premissa oculta:** as references viajam junto. No caminho de menor atrito, não viajam.
- **Tripwire:** se a instalação dominante for "só SKILL.md", embuta o essencial inline ou force o caminho completo.

### geo-content-brief (v1.0) — Tigre (perecível)
- **Falha:** GEO/AEO muda mensalmente; dados de "2025–2026" + estudo de Princeton podem virar conselho desatualizado com ar de autoridade.
- **Premissa oculta:** as heurísticas de citação de hoje valem no horizonte. Frágil num campo volátil.
- **Tripwire:** data de validade visível + revisão trimestral das faixas de citação.

### cowork-setup (v3.0) — Tigre (acoplada)
- **Falha:** mais acoplada a um produto novo e em mudança (Cowork); já reescrita v1→v3; depende de caminhos/estrutura que a Anthropic pode alterar.
- **Premissa oculta:** a estrutura de workspace do Cowork é estável. Não é.
- **Tripwire:** primeira a validar no CI de drift; é a que avisa quando o Cowork muda.

### Meta-elefante das sub-skills
As skills mais valiosas (premortem, llm-council, nem-parece-ia, cowork-setup) dependem de `references/` que **não viajam** no caminho de instalação de menor atrito. O README avisa "rodam melhor instaladas completas", mas o caminho 1 — o mais fácil e mais usado — entrega a versão degradada. Defeito de **distribuição** que mina a qualidade percebida exatamente nas skills da marca. É o gargalo da síntese do repo, em miniatura: o problema não é o conteúdo, é como ele chega.

---

*Gerado com a skill `premortem` da MSCREATIVE.SYSTEMS™ — método Gary Klein. 12/06/2026.*
