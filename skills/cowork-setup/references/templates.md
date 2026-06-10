# Templates de output — first-setup

Preencha com o material da entrevista. Regras transversais:

- Voz do aluno, não a sua. Reaproveite frases literais dele.
- Cada arquivo ≤ ~40 linhas. Corte antes de entregar.
- Lacuna sem material → `<!-- completar depois -->`. Nunca invente.
- Datas no formato DD/MM/AAAA. Inclua a linha de "última atualização" onde indicado.

---

## Modo mínimo viável → 1 arquivo: `claude.md`

```markdown
# CLAUDE.md — [Nome do aluno]

## Quem eu sou
[2-4 linhas: o que faz, pra quem, formato de trabalho. Presente, não biografia.]

## Prioridades agora
- [prioridade 1]
- [prioridade 2]
<!-- revisar a cada 2-3 meses -->

## Como eu escrevo
- Tom: [descrição curta com palavras do aluno]
- [pessoa, ritmo, maneirismos que usa]
- Nunca usar: [lista de banimentos]

## Como trabalhar comigo
- [regra de postura — ex: "questione minhas premissas"]
- [regra de contexto — ex: "pergunte antes de assumir"]
- [residuais: idioma, ferramentas, região]

## Projetos ativos (atualizar toda semana)
| Projeto | Status | Próximo passo | Prazo |
|---|---|---|---|
| [nome] | [status] | [ação] | [data ou —] |

*Última atualização: [data]*
```

---

## Modo completo → 4 arquivos

### `about-me.md`

```markdown
# Sobre mim

## O que eu faço
[2-4 linhas: profissão, público, formato de trabalho.]

## Minha semana
[1-3 linhas: sozinho/time, produção/reunião, gargalos.]

## Prioridades (próximos 2-3 meses)
- [prioridade 1]
- [prioridade 2]

*Última atualização: [data] — revisar a cada 2-3 meses*
```

### `writing-style.md`

```markdown
# Como eu escrevo

## Tom
[descrição com as palavras do aluno — ex: "seco, direto, zero cerimônia"]

## Padrões
- Pessoa: [1ª singular / nós / 3ª]
- Ritmo: [frases curtas / parágrafos longos / misto]
- [outros padrões extraídos da amostra, se houver]

## Amostra da minha voz
> [trecho real fornecido pelo aluno — se não houver: <!-- adicionar um trecho seu aqui -->]

## Banido
- [item 1]
- [item 2]
```

### `CLAUDE.md`

```markdown
# Instruções globais

1. [postura — ex: "Seja direto. Entregue, depois explique se eu pedir."]
2. [premissas — ex: "Questione minhas premissas quando vir furo."]
3. [contexto faltando — ex: "Pergunte antes de assumir."]
4. [idioma/formato — ex: "PT-BR. Respostas em markdown."]
5. [residuais da entrevista]
```

Regras em imperativo, máximo ~8. CLAUDE.md inchado é ignorado na prática — se a entrevista rendeu mais que 8 regras, escolha as que mudam comportamento de verdade.

### `PROJECTS.md`

```markdown
# Projetos ativos

*Última atualização: [data] — atualizar toda [dia da semana escolhido]*

## [Projeto 1]
- **Status:** [andamento / pausado / começando]
- **Próximo passo:** [ação concreta]
- **Prazo:** [data ou —]
- **Envolvidos:** [pessoas ou "só eu"]
- **Links:** [doc central ou —]

## [Projeto 2]
[mesma estrutura]
```

---

## Cartões de entrega

Diga o cartão no chat junto com cada arquivo. Adapte a redação ao tom da conversa, mas as 3 linhas são obrigatórias.

**`claude.md` consolidado (modo mínimo viável)**
- O que é: seu onboarding inteiro num arquivo só — quem você é, como fala, como o modelo trabalha com você e o que está rolando.
- O que NÃO é: definitivo. É o degrau 1; quando ele ficar apertado, você separa em 4 arquivos (próximas aulas).
- Quando atualizar: a seção de projetos TODA semana (dia fixo); o resto, a cada 2-3 meses ou quando deixar de ser verdade.

**`about-me.md`** (ou seção "Quem eu sou")
- O que é: a foto do seu presente profissional — o que o modelo precisa saber pra nunca te tratar como estranho.
- O que NÃO é: currículo. Passado só entra se mudar uma decisão de hoje.
- Quando atualizar: a cada 2-3 meses, ou quando uma prioridade da lista deixar de ser verdade.

**`writing-style.md`** (ou seção "Como eu escrevo")
- O que é: o manual da sua voz — o que faz um texto parecer SEU.
- O que NÃO é: lista de adjetivos ("profissional", "claro"). Sem exemplo concreto, não calibra nada.
- Quando atualizar: quase nunca. O sinal é ler um output e pensar "eu jamais escreveria assim" — aí falta uma regra aqui.

**`CLAUDE.md`** (ou seção "Como trabalhar comigo")
- O que é: as regras de operação — como o modelo deve se comportar com você, em qualquer conversa.
- O que NÃO é: depósito de desejos. Regra que não muda comportamento é ruído; menos é mais.
- Quando atualizar: quando você se pegar corrigindo o modelo pela MESMA coisa duas vezes — isso é uma regra pedindo pra existir.

**`PROJECTS.md`** (ou seção "Projetos ativos")
- O que é: o painel do agora — o que está rolando, próximo passo, prazo.
- O que NÃO é: arquivo morto. Projeto encerrado sai; histórico não mora aqui.
- Quando atualizar: TODA semana, dia fixo. É o único arquivo do setup que exige hábito — desatualizado, ele sabota os outros três.

## Tabela de manutenção (usar no fechamento)

No modo mínimo viável, troque "Arquivo" por "Seção do claude.md" — as cadências são as mesmas.

| Arquivo | Cadência | Sinal de que está velho |
|---|---|---|
| about-me | 2-3 meses | uma prioridade listada já não é verdade |
| writing-style | quase nunca | output soa "jamais escreveria assim" |
| CLAUDE.md | sob demanda | você corrigiu o modelo 2x pela mesma coisa |
| PROJECTS.md | **semanal (dia fixo)** | próximo passo listado já foi feito |

---

## Checklist antes de entregar

- [ ] Algum arquivo passou de 40 linhas? → cortar.
- [ ] about-me tem cheiro de currículo (datas passadas, "experiência em")? → reescrever no presente.
- [ ] writing-style tem adjetivo genérico ("profissional", "claro") sem exemplo concreto? → trocar por exemplo da entrevista.
- [ ] CLAUDE.md tem regra que não muda comportamento ("seja útil")? → deletar.
- [ ] PROJECTS.md tem projeto sem próximo passo? → voltar e perguntar.
