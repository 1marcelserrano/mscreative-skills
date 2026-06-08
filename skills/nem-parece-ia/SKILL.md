---
name: nem-parece-ia
description: Revisão editorial em português do Brasil para remover marcas de escrita artificial, vícios de IA, lero-lero corporativo, falsa profundidade, muletas retóricas e cadência robótica. Use ao escrever, reescrever, revisar ou diagnosticar textos pt-BR para torná-los mais naturais, específicos, diretos e adequados ao registro.
---

# Nem Parece IA

Usar esta skill para revisar textos em **português do Brasil** que soam artificiais, genéricos, inflados, previsíveis ou excessivamente “LLMizados”. O objetivo não é mascarar autoria, burlar detectores ou simular imperfeição humana. O objetivo é **melhorar clareza, especificidade, ritmo, responsabilidade sintática e naturalidade editorial**.

## Princípio central

Cortar o que anuncia, inflama ou teatraliza. Preservar o que informa, situa, prova ou move o texto.

Não aplicar regras cegas. Ajustar a revisão ao gênero, público e canal. Um post opinativo pode pedir cortes agressivos; uma documentação técnica pode precisar de passiva, enumeração e cautela; um texto institucional pode exigir diplomacia.

## Fluxo de revisão

1. **Identificar o registro** antes de editar: social/opinativo, ensaio, e-mail, institucional, técnico, acadêmico, comercial ou criativo.
2. **Detectar muletas pt-BR** em frases, aberturas, conectores, intensificadores, jargões e metacomentários.
3. **Diagnosticar estruturas artificiais**: contraste fabricado, falsa agência, passiva evasiva, abstração vaga, pergunta performática e punchline automática.
4. **Reescrever com agente, ação e objeto**: nomear quem faz, o que faz, por que importa e qual consequência concreta aparece.
5. **Regular o ritmo**: alternar frase curta, média e longa; evitar tríades previsíveis; não encerrar todo parágrafo com frase de efeito.
6. **Preservar nuance quando ela trabalha**: não cortar advérbios, modalizadores, passivas ou conectores quando eles carregam precisão, escopo, cortesia ou rigor.
7. **Entregar duas camadas quando útil**: diagnóstico curto dos padrões encontrados e versão revisada do texto.

## Regras centrais

| Regra | Aplicação |
|---|---|
| Cortar abertura vazia | Remover “é importante destacar”, “vale ressaltar”, “quando falamos de”, “no cenário atual” quando só atrasam o ponto. |
| Trocar abstração por evidência | Substituir “impacto significativo” por qual impacto, em quem, quando e com que efeito. |
| Nomear o agente | Trocar “o mercado exige” por “clientes B2B recusam contratos sem SLA”. |
| Reduzir contraste performático | Trocar “não é sobre X, é sobre Y” por uma afirmação direta de Y, exceto quando o contraste realmente organiza a tese. |
| Cortar falsa profundidade | Remover “isso muda tudo”, “o ponto é simples”, “a verdade é que” se não acrescentam prova. |
| Remover lero corporativo | Trocar “alavancar sinergias para entregar valor” por verbos verificáveis. |
| Controlar intensificadores | Cortar “muito”, “profundamente”, “realmente”, “simplesmente”, “genuinamente” quando só aumentam volume. |
| Variar cadência | Evitar sequência de frases com mesma extensão, tríades automáticas e parágrafos terminados sempre em punchline. |
| Respeitar registro | Aplicar cortes conforme o gênero textual, sem transformar tudo em manifesto seco. |

## Checklist rápido

Antes de entregar o texto revisado, verificar:

- Há abertura que poderia ser apagada sem perda de sentido?
- Há frase que anuncia importância em vez de demonstrá-la?
- Há sujeito abstrato fazendo ação humana?
- Há jargão que poderia virar verbo concreto?
- Há contraste “não é X, é Y” usado como efeito?
- Há pergunta retórica respondida logo em seguida?
- Há três itens onde um ou dois bastariam?
- Há advérbio que infla em vez de especificar?
- Há parágrafo encerrando com frase de efeito previsível?
- A revisão preservou o registro adequado ao contexto?

## Rubrica de pontuação

Avaliar de 1 a 10 em cada dimensão.

| Dimensão | Pergunta |
|---|---|
| Direção | O texto chega ao ponto sem anunciar que chegará ao ponto? |
| Concretude | O texto nomeia agentes, ações, objetos e consequências? |
| Naturalidade | O texto soa como português brasileiro escrito por pessoa fluente? |
| Ritmo | A cadência varia conforme a ideia, sem metrônomo de IA? |
| Adequação | O texto respeita gênero, canal, público e nível de formalidade? |

Abaixo de 35/50, revisar profundamente. Entre 35 e 42, corrigir padrões dominantes. Acima de 42, fazer polimento localizado.

## Referências sob demanda

Ler apenas os arquivos necessários para a tarefa atual.

| Arquivo | Quando carregar |
|---|---|
| `references/frases-ptbr.md` | Quando precisar detectar muletas, conectores vazios, jargão, intensificadores e frases prontas. |
| `references/estruturas-ptbr.md` | Quando o problema estiver na forma argumentativa, na sintaxe, na agência ou na arquitetura do parágrafo. |
| `references/ritmo-ptbr.md` | Quando o texto soar robótico, performático, metrônomico, com frases de efeito ou cadência previsível. |
| `references/registros.md` | Quando precisar calibrar a revisão para gênero textual específico. |
| `references/exemplos.md` | Quando precisar de modelos de antes/depois para guiar a reescrita. |
| `references/checklist.md` | Quando precisar de uma auditoria rápida ou uma ordem objetiva de edição. |
| `references/atribuicao-e-uso.md` | Quando precisar esclarecer inspiração, licença conceitual e uso responsável. |

## Formato de resposta recomendado

Quando o usuário pedir revisão simples, entregar apenas a versão revisada. Quando pedir diagnóstico, usar este formato:

```markdown
## Diagnóstico

O texto usa [padrões principais]. O maior problema é [problema dominante].

## Revisão

[texto revisado]

## Principais mudanças

| Antes | Depois | Motivo |
|---|---|---|
| ... | ... | ... |
```

## Atribuição conceitual

Esta skill foi criada como adaptação editorial brasileira inspirada no projeto público `hardikpandya/stop-slop`, licenciado sob MIT. A versão pt-BR recria a taxonomia para padrões linguísticos brasileiros, em vez de traduzir mecanicamente os exemplos e gatilhos do inglês.
