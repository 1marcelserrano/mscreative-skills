# Workspace completo — guia da Rota 2

Herdado da cowork-setup V2 (fases 2-9), destilado. Use módulo a módulo; não despeje tudo de uma vez no usuário.

## 1. Estrutura de pastas

```
[Raiz do workspace]/
├── ABOUT_ME/           ← Quem você é + o que está na sua mesa. READ-ONLY.
│   ├── about-me.md
│   ├── writing-style.md
│   ├── PROJECTS.md     ← Dashboard do trabalho ativo. Refresh semanal.
│   └── (arquivos de contexto opcionais)
├── PROJECTS/           ← Profundidade por projeto. Uma subpasta por projeto. READ-ONLY.
├── TEMPLATES/          ← Padrões comprovados pra reusar. READ-ONLY.
├── KNOWLEDGE/          ← Base de conhecimento destilada (módulo 5). READ-ONLY.
└── CLAUDE_OUTPUTS/     ← Onde o Claude entrega. ÚNICA pasta de escrita.
```

Por quê: read-only + 1 zona de escrita = contenção de dano. Se o usuário já tem outra estrutura, adapte — o princípio (contexto read-only + uma zona de escrita + distinção arquivo/pasta) importa mais que os nomes.

**Naming de outputs:** `PROJETO_TIPO_V1.ext` (ex: `ACME_REPORT_V1.md`). Sempre versionar; nunca sobrescrever sem incrementar.

## 2. A distinção crítica (erro nº 1 dos setups)

- **`PROJECTS.md`** (arquivo, em ABOUT_ME/) — dashboard macro. 1 página. O que está acontecendo AGORA.
- **`PROJECTS/`** (pasta, na raiz) — mergulho. Briefs, transcrições, decisões de UM projeto.

Coexistem. Nomeie a confusão explicitamente ao montar. Nunca inche o PROJECTS.md com conteúdo que pertence à pasta.

## 3. PROJECTS.md — template dashboard

```markdown
# Projetos ativos

Última atualização: [data]

## 🟢 EM ANDAMENTO

### [Nome do projeto]
- **Status:** [1 frase — onde está]
- **Próximo passo:** [o que está pendente e quando]
- **Deadline crítico:** [data ou "sem data dura"]
- **Envolvidos:** [quem mais participa]
- **Links:** [pasta, doc, brief]
- **Bloqueios:** [só se houver — omita senão]

## 🟡 PAUSADO
### [Projeto] — pausado porque [razão concreta], retoma [quando]

## 🔵 ENTRANDO (próximos 30 dias)
- [Projeto] — começa [quando]

## ⚫ FECHADO RECENTE (últimos 30 dias)
- [Projeto] — fechado [data] — [resultado em 1 linha]
```

Regras duras: máximo 1 página · 5-7 ativos no teto (mais = fragmentação) · status em 1 frase · "próximo passo" é o coração — parado 2 semanas = projeto travado, o arquivo expõe isso. O que NÃO é: histórico, brainstorm de ideias, briefs detalhados (pasta), lista de micro-tarefas.

## 4. CLAUDE.md — starter V2 (Global Instructions)

Settings → Cowork → Edit Global Instructions. ≤150 linhas (mais curto = mais obediência). Suporta imports `@caminho`.

```markdown
# INSTRUÇÕES GLOBAIS

## ANTES DE TODA TAREFA
1. Leia ABOUT_ME/about-me.md e ABOUT_ME/writing-style.md. Nenhuma tarefa começa sem.
2. Leia ABOUT_ME/PROJECTS.md pra saber o que está ativo. Tarefa ligada a projeto
   listado → PROJECTS.md é contexto operacional primário.
3. Tarefa de projeto → leia TAMBÉM a subpasta PROJECTS/{projeto}/ pra profundidade.
4. Tipo de conteúdo com padrão em TEMPLATES/ → estude o template primeiro.

## PROTOCOLO DE PASTAS
Read-only: ABOUT_ME/ · TEMPLATES/ · PROJECTS/ · KNOWLEDGE/
Escrita: CLAUDE_OUTPUTS/ (espelhe a estrutura de PROJECTS/)

## DISTINÇÃO: PROJECTS.md vs PROJECTS/
- ABOUT_ME/PROJECTS.md = dashboard macro (1 página, refresh semanal)
- PROJECTS/{projeto}/ = profundidade por projeto
Nunca confunda. Nunca inche o dashboard com conteúdo da pasta.

## NAMING
PROJETO_TIPO_V1.ext · incremente versão · nunca sobrescreva

## REGRAS DE OPERAÇÃO
- Brief confuso → AskUserQuestion. Não preencha lacuna com enchimento.
- Tarefa cita projeto fora do PROJECTS.md → sinalize (pode estar desatualizado).
- Entregue o trabalho. Guarde comentário pra quando pedirem.
- Nunca delete arquivo.
- Antes de entregar, confira voz contra about-me.md e writing-style.md.
```

**Roteamento por projeto (só com 3+ projetos ativos com regras diferentes):** seção `## PROJECT ROUTING` inline, 3-5 linhas por projeto (o que carregar sempre, tom, naming). Atenção: `.claude/rules/` com frontmatter `paths:` funciona no Claude Code CLI mas NÃO no Cowork — no Cowork, regra de projeto vai inline no CLAUDE.md.

## 5. KNOWLEDGE/ — base de conhecimento

Conhecimento destilado e reutilizável entre projetos. **Ao apresentar a KNOWLEDGE/, ancore SEMPRE na tabela das três moradas** — é a vacina contra a pasta virar despejo:

| Onde | O que mora | Cadência |
|---|---|---|
| `ABOUT_ME/PROJECTS.md` | O que está na mesa AGORA | Semanal |
| `PROJECTS/{projeto}/` | Fundo de UM projeto (briefs, decisões) | Por projeto |
| `KNOWLEDGE/` | O que sobrevive aos projetos | Cresce devagar |

Dois arquivos de partida:

```markdown
# KNOWLEDGE — _INDEX.md
## DOMAIN (o que as coisas são)
| Arquivo | Cobre |
## PROCEDURAL (como fazer)
| Arquivo | Cobre |
## ERRORS
Log classificado de erros recorrentes → ERRORS.md
```

```markdown
# ERRORS.md — log classificado
## Classificação
[CONTEXTO] faltou contexto · [PREMISSA] assumiu errado · [VOZ] saiu da voz ·
[ESCOPO] fez demais/de menos · [FONTE] usou fonte errada
## Log
- [data] [TIPO] — o que aconteceu → regra extraída
```

Regra de ouro: NÃO despeje arquivos brutos. PDF de 50 páginas → brief de 1 página. Extraia sinal.

## 6. Ritual semanal (10 min, dia fixo)

O PROJECTS.md é o único arquivo de cadência semanal. Sem ritual, morre. Ensine explicitamente antes de declarar o setup completo:

> "Toda [sexta], 10 minutos: atualize o status de cada ativo · mova concluídos pra Fechado Recente · mova travados pra Pausado com razão real e data de retomada · suba os de Entrando que começaram · apague Fechados com 30+ dias. Pular 2 semanas = o arquivo está mentindo pro Claude. Claude confiando em arquivo mentiroso é pior que sem arquivo."

Sugira bloco recorrente no calendário: "[Sexta] 16h — PROJECTS.md refresh, 10 min".

## 7. Auto memory

O Claude tem memória entre sessões (`/memory`). Ensine: ao fim de sessões importantes, "salve o que aprendeu sobre minhas preferências na memória".

- **Guardar:** preferências estáveis, correções que o usuário fez, convenções recorrentes.
- **NÃO guardar:** estado de projeto (é o PROJECTS.md — os dois sistemas brigam se misturar), conteúdo de referência longo (pastas existem pra isso), senhas/chaves.

## 8. Prompt template universal

```
Quero [TAREFA] para [CRITÉRIO DE SUCESSO].
Primeiro, cheque o PROJECTS.md pra ver se isso conecta com trabalho ativo.
Depois me faça perguntas com AskUserQuestion. Refine a abordagem comigo
antes de executar.
```

Muda o default de "pergunte tudo ao usuário" pra "cheque o contexto ativo primeiro, pergunte só o que falta". Dica Mac: atalho de Text Replacement que cola o template.

## 9. Plugins e conectores

| Tipo de trabalho | Plugins |
|---|---|
| Marketing/Conteúdo | Marketing, Productivity |
| Vendas/BD | Sales, Productivity |
| Consultoria | Productivity, Data analysis |
| Jurídico | Legal, Productivity |
| Engenharia | Engineering, Data analysis |
| Pesquisa | Enterprise search, Productivity |

Conectores (Slack, Drive, Notion, Gmail, Calendar): Settings → Connectors. Só os que a pessoa realmente usa.

## 10. Higiene de contexto (ensine as 5 regras)

1. `/clear` entre tarefas não relacionadas.
2. Arquivos enxutos: about-me 300 palavras · writing-style 200 · PROJECTS.md 1 página · CLAUDE.md 150 linhas.
3. Nada de arquivo bruto em PROJECTS/ — extraia sinal.
4. Uma tarefa complexa por sessão.
5. Subagents pra investigação; conversa principal limpa.

## Fluxo guiado de 35 minutos (quando pedirem o passo a passo)

0-5 install/abrir · 5-12 identidade+voz · 12-20 PROJECTS.md + ritual · 20-25 CLAUDE.md · 25-30 primeira tarefa real tocando um projeto do dashboard · 30-35 plugin + conectores + briefing de higiene. Teste final: "Escreva um email curto sobre [projeto do PROJECTS.md]. Soa como você E sabe o que está acontecendo?"
