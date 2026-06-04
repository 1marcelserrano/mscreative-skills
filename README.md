# mscreative-skills

**Skills públicas da MSCREATIVE.SYSTEMS™ para o Claude. Ferramentas de decisão, em português.**

[Instalar](#instalar) • [Skills](#skills-disponíveis) • [Em destaque: premortem](#em-destaque-premortem)

---

Uma coleção curada de skills para o Claude (Claude Code, Cowork e claude.ai). Cada skill é uma ferramenta de pensamento — testada em uso real, escrita em PT-BR, sem firula. Instale a que precisar.

## Skills disponíveis

| Skill | Versão | O que faz | Triggers principais |
|---|---|---|---|
| [`premortem`](./skills/premortem/) | v1.0 | Assume que seu plano já falhou e descobre por quê antes de você gastar dinheiro, tempo ou reputação. | `roda um premortem`, `o que pode matar isso`, `onde isso quebra`, `que ponto cego eu tenho`, `fura esse plano` |

## Instalar

```bash
# Manual (qualquer skill da coleção)
git clone https://github.com/1marcelserrano/mscreative-skills.git
cp -r mscreative-skills/skills/premortem ~/.claude/skills/
```

Reinicie a sessão do Claude. A skill dispara sozinha quando o contexto bate — ou chame pelo nome.

---

## Em destaque: premortem

Um postmortem investiga por que algo morreu depois que morreu. O premortem faz o oposto: você imagina que já falhou e descobre por quê antes de começar. Método de Gary Klein (Harvard Business Review), a técnica de decisão que Daniel Kahneman chamou de sua mais valiosa.

### Como funciona

| Antes | Depois |
|---|---|
| Você pergunta "esse plano é bom?" e o modelo acha razões pra dizer sim. | A premortem assume que o plano já morreu e te entrega os riscos reais, a premissa que você não questionou e tripwires datados — antes de você gastar. |

O modelo para de procurar razões pro seu plano funcionar e passa a explicar como ele desmoronou.

### Quando usar

- Um lançamento com dinheiro ou reputação em jogo
- Uma mudança de pricing ou de modelo de negócio
- Uma contratação cara prestes a acontecer
- Um pivô de estratégia ou posicionamento
- Qualquer decisão onde errar custa caro — e que ainda dá pra mudar de rumo

Linguagem natural também dispara — ex.: "to a ponto de contratar meu primeiro head of growth, me ajuda a ver os pontos cegos antes de fechar".

### O que entrega

- **Triagem Tigre / Tigre de Papel / Elefante** — separa ameaça real (com evidência) do que só assusta, e nomeia o que você está evitando falar.
- **Matriz Probabilidade × Impacto** — prioriza onde focar, sem achismo.
- **Visão de fora (base rates)** — "decisões como esta falham X% das vezes", pra ancorar a imaginação na taxa histórica real.
- **Tripwires datados** — gatilhos com data e ação ("se até DD/MM X não acontecer → pivota"), decididos a frio.
- **Plano revisado** — sequenciado pelo menor experimento que falsifica sua premissa mais arriscada primeiro.
- **Relatório HTML** — visual, escaneável, pra revisitar a decisão depois.

### Por que funciona

- **Honestidade forçada** — o enquadramento "isso já morreu" quebra o otimismo cordial do modelo, que por padrão acha razões pra concordar com você.
- **Triagem que prioriza** — nem todo medo merece a mesma energia; a classificação separa o Tigre real do Tigre de Papel.
- **Saída acionável** — plano revisado, tripwires com data e relatório, não conselho genérico que serve pra qualquer coisa.

---

## Contribuindo

PRs são bem-vindos. Abra uma issue antes de mudanças grandes.

## Licença

MIT — veja [LICENSE](./LICENSE).

---

<sub>Forjado na [MSCREATIVE.SYSTEMS™](https://mscreative.systems) — Barcelona</sub>
