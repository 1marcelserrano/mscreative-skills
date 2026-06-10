# Roteiros de entrevista — first-setup

Dois roteiros. Use o que a Fase 1 definiu. Cada pergunta traz a INTENÇÃO — entenda o que ela precisa extrair e adapte a formulação ao tom da conversa. Não leia as perguntas como script robótico.

Legenda: **[W]** = fechada, via AskUserQuestion · **[T]** = aberta, texto livre.

---

## Roteiro A — Mínimo viável (6 perguntas → 1 claude.md)

**A1. [T] O que você faz e pra quem?**
Intenção: a frase de abertura do arquivo. Profissão + público/mercado + formato de trabalho (CLT, freela, fundador, estúdio). Se vier currículo, redirecionar pro presente.

**A2. [T] O que está tentando fazer acontecer nos próximos 2-3 meses?**
Intenção: prioridades atuais. 1 a 3 itens. É o que diferencia about-me de CV.

**A3. [T] Como você escreve? Me dá exemplos do seu tom — e me diz o que te irrita em texto de IA.**
Intenção: matéria-prima do estilo. Capturar: pessoa (1ª/3ª), ritmo (curto/longo), palavras que usa, palavras/maneirismos que bane. Se o aluno travar, ofereça contraste: "mais 'oi, time' ou mais 'prezados'?". Follow-up útil: pedir um trecho real de algo que ele escreveu e gostou.

**A4. [W] Quando eu (Claude) trabalhar com você, qual postura prefere?**
Opções: (a) Direto ao ponto — entrega e pronto · (b) Consultivo — questione minhas premissas e aponte furos · (c) Didático — explique o raciocínio enquanto faz. MultiSelect ok (a+b é combo comum).

**A5. [T] Quais projetos estão ativos AGORA? Pra cada um: próximo passo e prazo, se tiver. E que dia da semana você reserva 5 minutos pra atualizar essa lista?**
Intenção: seção de projetos. 1-4 projetos, cada um com status + próximo passo. Sem histórico. O dia fixo entra no cabeçalho da seção — perguntar aqui evita editar o arquivo depois do fechamento.

**A6. [W] Algum contexto que eu deva sempre lembrar?**
Opções: (a) Não, fechamos · (b) Sim, idioma/região específicos · (c) Sim, ferramenta/stack que sempre uso · (d) Sim, outra coisa (campo livre). Intenção: pescar o residual que as outras perguntas não pegaram.

---

## Roteiro B — Estrutura completa (10-12 perguntas → 4 arquivos)

Ritmo de entrega: ao FECHAR cada bloco, gere e entregue o arquivo daquele bloco (com cartão de entrega) antes de abrir o próximo. O aluno valida em pedaços pequenos e vê payoff durante a entrevista, não só no fim.

### Bloco Identidade → about-me.md

**B1. [T]** = A1 (o que faz e pra quem).
**B2. [T]** = A2 (prioridades 2-3 meses).
**B3. [T] Como é sua semana típica de trabalho?**
Intenção: contexto operacional — sozinho ou em time, reuniões ou produção, gargalos. Ajuda o modelo a calibrar sugestões à realidade do aluno.

### Bloco Voz → writing-style.md

**B4. [T]** = A3 (tom + irritações com texto de IA).
**B5. [T] Me manda um trecho curto de algo que VOCÊ escreveu e representa bem sua voz.**
Intenção: amostra real pra extrair padrões (tamanho de frase, vocabulário, pontuação). Se o aluno não tiver nada à mão, pule sem culpa.
**B6. [W] Lista de banimentos — o que NUNCA deve aparecer no seu texto?**
Opções multiSelect: (a) Emojis · (b) Clichês corporativos (alavancar, sinergia, robusto) · (c) Frases-morta ("nos dias de hoje", "vale ressaltar") · (d) Tom de vendedor/hype. Campo Other pra adições.

### Bloco Operação → CLAUDE.md

**B7. [W]** = A4 (postura de trabalho).
**B8. [W] Quando faltar contexto numa tarefa, o que prefiro que eu faça?**
Opções: (a) Pergunte antes de fazer · (b) Faça com o que tem e marque as suposições · (c) Depende — pergunte só se for decisão difícil de reverter.

### Bloco Projetos → PROJECTS.md

**B9. [T]** = A5 (projetos ativos, próximo passo, prazo).
**B10. [T] Pra cada projeto: quem mais está envolvido? Algum link/documento central? E qual dia da semana você consegue reservar 5 minutos pra atualizar este painel?**
Intenção: stakeholders + links + o dia fixo que entra no cabeçalho do PROJECTS.md (perguntar AQUI, antes de gerar o arquivo). Se o aluno trabalha sozinho e sem docs, registre isso e siga.

### Fechamento

**B11. [W]** = A6 (contexto residual).
**B12. [T] (opcional)** Se alguma resposta anterior ficou ambígua, este é o slot do follow-up final. Se nada pendente, pule direto pra Fase 3.

---

## Calibragem durante a entrevista

- Material da Fase 0.5 (redes/posts) ou de um claude.md anterior já responde uma pergunta → transforme-a em confirmação de 1 linha ("pelos seus posts, X — bate?"). Exceção: A2/B2 (prioridades) sempre é perguntada de verdade.
- Resposta rica que cobre 2 perguntas → pule a redundante e avise ("você já me respondeu a próxima, vou pular").
- Resposta de uma linha em pergunta-chave (A1, A3, A5) → UM follow-up específico, não genérico. "Me dá um exemplo" funciona melhor que "pode detalhar?".
- Aluno ansioso pra terminar → corte as opcionais (B3, B5, B10), nunca as estruturais.
- Aluno se estendendo demais → ótimo sinal, não interrompa. Material demais é problema bom; você corta na síntese.
