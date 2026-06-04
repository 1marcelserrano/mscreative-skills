# Método canônico do premortem

Carregue este arquivo quando precisar dos critérios detalhados de triagem (Passo 2.5) ou do template do relatório HTML (Passo 5). O SKILL.md tem o fluxo; aqui está a profundidade.

## Índice
- §origem — de onde vem o método e por que funciona
- §triagem — Tigre / Tigre de Papel / Elefante, critérios completos
- §base-rates — como estimar a visão de fora
- §tripwires — como escrever um gatilho que funciona
- §relatório — template e design do HTML

---

## §origem

Gary Klein publicou o premortem em "Performing a Project Pre-Mortem", Harvard Business Review (2007). A base cognitiva é o trabalho de Deborah Mitchell, Jay Russo e Nancy Pennington sobre "prospective hindsight" (1989): pedir que as pessoas imaginem um evento futuro como se já tivesse ocorrido aumenta em ~30% a capacidade de identificar razões corretas para o resultado.

Daniel Kahneman tratou o premortem em "Rápido e Devagar" (2011) como antídoto para o excesso de confiança e o pensamento de grupo. A lógica: dentro de uma equipe que já abraçou um plano, levantar dúvidas soa como deslealdade. O premortem legitima a dúvida — todo mundo é convidado a imaginar o fracasso, então apontar fraquezas vira o jogo, não traição.

A camada Tigre / Tigre de Papel / Elefante vem da prática de gestão de produto (popularizada em discovery de produto) e serve para triar o output bruto do premortem: nem todo medo levantado merece a mesma energia.

Leituras de apoio:
- Gary Klein, "Performing a Project Pre-Mortem", HBR (2007)
- Daniel Kahneman, "Rápido e Devagar" (2011) — hindsight prospectivo
- Chip & Dan Heath, "Decisive" (2013) — decisão sob incerteza
- Amy Edmondson, "The Fearless Organization" (2018) — segurança psicológica para expor elefantes

---

## §triagem

Depois do premortem bruto, classifique cada motivo de falha. A triagem evita dois erros opostos: tratar todo medo como ameaça mortal (paralisia) e ignorar a ameaça real porque ela veio embrulhada em desconforto.

### Tigre — ameaça real

Características:
- Sustentado por dado, experiência passada ou tendência observável
- Dá pra descrever um cenário de falha plausível em termos concretos
- Ignorar seria negligência

Exemplos:
- "O serviço de pagamento caiu 3 vezes no último mês. Queda no dia do lançamento é plausível."
- "Temos zero clientes no segmento enterprise e o time comercial não tem relacionamento nenhum lá."
- "A regulação entra em vigor em 60 dias e a gente nem começou o compliance."

Todo Tigre recebe urgência:

| Urgência | Definição | Ação |
|---|---|---|
| **Bloqueia-Lançamento** | Se não resolver, não lança. | Plano de mitigação, dono e data de decisão antes do lançamento. |
| **Fast-Follow** | Resolve em até 2 semanas pós-lançamento. | Plano documentado, dono, agendado pro primeiro ciclo. |
| **Monitorar** | Acompanha e ataca se escalar. | Entra no registro de risco, revisão em cadência. |

### Tigre de Papel — assusta, mas não morde

Características:
- Baseado em hipótese sem evidência de apoio
- Probabilidade muito baixa, ou impacto gerenciável
- Geralmente vem de ansiedade geral, não de conhecimento específico

Exemplos:
- "Um concorrente pode copiar a feature" — possível, mas o ciclo de execução dele é de 6-12 meses.
- "O servidor pode não aguentar 100x de tráfego" — mas a projeção real é 5x, com auto-scaling.
- "Os usuários podem odiar a UI nova" — mas o teste com 8 pessoas mostrou satisfação alta.

Registre e siga. Não gaste energia de mitigação aqui — o custo de oportunidade é o erro.

### Elefante — o que ninguém fala

Características:
- O time evita por política, hierarquia ou desconforto
- Costuma ser gente, processo ou ego, não técnica
- É a causa real de falha com mais frequência do que se admite

Exemplos:
- "O tech lead não acredita no projeto e está desengajado há semanas."
- "A feature favorita do CEO dita o roadmap, mas nenhum cliente pediu."
- "Não temos plano pra quando o contrato do prestador acabar mês que vem."

Para founder ou criador solo, o elefante quase sempre é uma destas formas:
- A premissa em que ele está emocionalmente investido (a audiência que ele *quer* ter, não a que tem)
- O trabalho que ele evita porque é chato ou assustador (vendas, suporte, distribuição)
- A dúvida sobre si mesmo que ele não verbaliza ("será que eu sou a pessoa certa pra isso?")

Tratamento do elefante (diferente do Tigre):
1. **Nomear** — diga em voz alta. "A preocupação não-dita aqui é que..."
2. **Reavaliar** — é um Tigre disfarçado? Se sim, reclassifique e dê evidência.
3. **Decidir** — ataca (atribui dono) ou aceita conscientemente (documenta a aceitação e o porquê).

---

## §base-rates

A visão de fora (outside view, Kahneman) pergunta: "decisões da mesma classe que esta, quantas falham?" Em vez de avaliar este plano pelos seus méritos internos (visão de dentro, otimista por padrão), você o compara com a classe de referência.

Como fazer:
1. **Defina a classe de referência.** Não "meu lançamento", mas "lançamentos de curso ao vivo de ticket alto pra audiência fria".
2. **Busque a taxa.** Se há dado público ou histórico do próprio usuário, cite. Se não, estime com lógica explícita — é melhor um número honesto com raciocínio do que nenhum.
3. **Compare.** Se a base rate de sucesso é 20% e o usuário está 80% confiante, o gap é o prêmio do premortem.

Faixas de referência úteis (estimativas grosseiras, ajuste ao caso):
- Startups que chegam a retorno relevante: ~10%
- Features novas que movem a métrica-alvo: ~10-30%
- Lançamentos de produto digital pra lista própria engajada: ~2-10% de conversão
- Lançamentos pra audiência fria: ~1-3%
- Contratações sênior que dão certo no primeiro ano: ~50-65%

Sempre marque a estimativa como estimativa. O ponto não é precisão — é tirar o usuário da visão de dentro.

---

## §tripwires

Um tripwire é um gatilho pré-combinado que dispara uma decisão. Substitui "sinal de alerta" vago por compromisso concreto, decidido a frio — antes do calor do momento, quando o viés de custo afundado te prende.

Anatomia de um bom tripwire:
- **Métrica ou evento observável** — algo que você mede ou vê, não uma sensação
- **Data** — até quando
- **Ação** — o que acontece se disparar: parar, pivotar, dobrar a aposta

Formato: "Se até [data] [métrica/evento] [limiar], então [ação]."

Exemplos:
- "Se até 15/03 menos de 10 inscritos forem gestores de time, o alvo está errado → pivota a oferta pra solopreneur."
- "Se na primeira semana o churn passar de 8%, paro o tráfego pago e investigo o onboarding."
- "Se em 30 dias o novo contratado não tiver fechado o primeiro ciclo sozinho, abro conversa de recalibração."

O tripwire decidido antes é honesto. O tripwire decidido no calor é racionalização.

---

## §relatório

Gere um arquivo HTML único, autocontido, com CSS inline. Não use framework, não puxe nada de CDN.

Princípios de design:
- **Fundo escuro** (#0a0e1a ou similar), tipografia limpa, fácil de escanear
- **A síntese no topo** — falha mais provável, falha mais perigosa, premissa oculta, base rate, plano revisado, tripwires, elefantes, confiança revisitada. É o que mais gente lê.
- **Matriz P×I como visual central** — grid 2×2, eixo X = Probabilidade (Baixa→Alta), eixo Y = Impacto (Baixo→Alto). Posicione cada Tigre como um ponto/card. Canto superior-direito destacado.
- **Um card por modo de falha** — header com o motivo, depois a história da falha, a premissa subjacente e os tripwires. Cor por classificação:
  - Tigre → vermelho/laranja (#ff4d4d / #ff8c42)
  - Tigre de Papel → amarelo apagado (#c9a227)
  - Elefante → roxo/cinza (#8c7ae6)
- **Indicador de severidade** visível em cada card (badge de urgência: Bloqueia-Lançamento / Fast-Follow / Monitorar)
- **Visão geral dos agentes** — mostre quantos agentes rodaram e o escopo, em grid, pro usuário ver a varredura completa de relance
- **Confiança antes → depois** — um número grande mostrando o delta
- **Rodapé** com timestamp e o que foi premortemado

Estrutura sugerida do documento:
1. Cabeçalho: "PREMORTEM — [o que foi premortemado]" + data + horizonte
2. Bloco síntese (os 9 itens)
3. Matriz P×I
4. Cards de falha (Tigres primeiro, depois Tigres de Papel, depois Elefantes)
5. Rodapé

Abra o arquivo depois de gerar.
