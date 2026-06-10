# Diagnóstico — checklist da Rota 3

Herdado da cowork-setup V2 (fase 10 + diagnosis mode). Leia os arquivos existentes ANTES da primeira pergunta.

## Abertura

Uma pergunta só: "Vi que você já tem [X, Y]. O que não está funcionando? O que parece errado?" A resposta orienta a ordem da auditoria — mas audite tudo.

## Checklist de auditoria

| Check | Pergunta | Conserto |
|---|---|---|
| Estrutura | Padrão read-only + 1 pasta de escrita? | Reestruturar (workspace.md §1) |
| about-me.md | Existe? ≤300 palavras? Amostra de voz real? Específico? | Reescrever ou criar — gap profundo → ofereça a entrevista da Rota 1 |
| writing-style.md | Existe? Palavras proibidas? Regras de voz? Exemplo bom/ruim? | Idem |
| PROJECTS.md | Existe? ≤1 página? 3-7 ativos com status + próximo passo? Atualizado ≤14 dias? | Criar ou refresh agora |
| CLAUDE.md | ≤150 linhas? Referencia estrutura E PROJECTS.md? | Reescrever (workspace.md §4) |
| Distinção arquivo/pasta | Usuário entende PROJECTS.md vs PROJECTS/? Sem inchaço nos dois? | Re-explicar (workspace.md §2) |
| Ritual semanal | Bloco no calendário? Usuário comprometido? | Configurar agora (workspace.md §6) |
| Higiene | ABOUT_ME/ ≤1.500 palavras? Arquivo bruto despejado? | Cortar; extrair sinal |
| KNOWLEDGE/ | Existe? Indexado? Ou conhecimento espalhado em chats? | Montar (workspace.md §5) |
| Templates | Padrões pros entregáveis recorrentes? | Criar starters |
| Naming | Formato consistente `PROJETO_TIPO_V1.ext`? | Aplicar convenção |
| Auto memory | Conhece `/memory`? Não usa pra estado de projeto? | Explicar (workspace.md §7) |
| Plugins | Os relevantes instalados? | Recomendar (workspace.md §9) |

**Gravidade:** PROJECTS.md parado 14+ dias = gap crítico, mesma severidade de about-me ausente. O arquivo mentindo é pior que o arquivo faltando.

## Regra de conduta

Para cada gap: **ofereça consertar agora**. Não entregue lista de problemas — resolva na sessão. Priorize: (1) arquivo mentiroso ou ausente da camada pessoal, (2) ritual, (3) estrutura, (4) o resto.

## Erros comuns (nomeie quando encontrar)

- **Sessão pia-de-cozinha** — tudo num chat só. Conserto: `/clear` entre tarefas.
- **CLAUDE.md superespecificado** — manual de 500 linhas. Conserto: ≤150.
- **PROJECTS.md fóssil** — 3+ semanas parado. Conserto: ritual de sexta.
- **Confusão PROJECTS.md ↔ PROJECTS/** — brief no dashboard ou status na pasta. Conserto: workspace.md §2.
- **Confiar sem revisar** — enviar output sem ler. Conserto: revisão sempre.

## Fechamento

Recapitule o que foi consertado vs o que ficou pendente (com dono e data). Setup não é monte-e-esqueça: about-me revisita trimestral, PROJECTS.md semanal, CLAUDE.md evolui por irritação — cada vez que o Claude erra do mesmo jeito, vira regra nova.
