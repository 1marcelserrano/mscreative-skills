# nem-parece-ia

**Revisão editorial em PT-BR para tirar cara de IA, lero-lero corporativo e cadência robótica de textos.**

`nem-parece-ia` é uma skill para reescrever, revisar ou diagnosticar textos em português do Brasil que soam genéricos, inflados, artificiais, performáticos ou excessivamente parecidos com saída de LLM. Ela não tenta “enganar detector”; ela melhora texto ruim: corta abertura vazia, troca abstração por evidência, nomeia agente, regula ritmo e adapta o registro ao canal.

A lógica foi inspirada no projeto público [`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop), mas a versão aqui foi reconstruída para padrões linguísticos brasileiros: vícios de LinkedIn em PT-BR, jargão corporativo local, falsa profundidade, estruturas de contraste, ritmo traduzido do inglês e muletas comuns em textos institucionais, técnicos, acadêmicos e comerciais.

---

## Quando usar

Use quando você tiver um rascunho que parece correto, mas sem vida; claro, mas genérico; bem formatado, mas com cheiro de IA. A skill funciona bem para posts, artigos, e-mails, textos institucionais, landing pages, propostas, apresentações, scripts, relatórios e trechos acadêmicos que precisam de mais naturalidade e precisão.

| Bom alvo | Mau alvo |
|---|---|
| Texto em PT-BR que soa artificial | Pedido para burlar detector de IA |
| Copy cheia de jargão e promessa vaga | Texto em outro idioma sem adaptação para PT-BR |
| Post com “não é sobre X, é sobre Y” | Texto literário em que a artificialidade é intencional |
| E-mail longo sem pedido claro | Revisão puramente gramatical, sem problema de voz |
| Institucional com “excelência, inovação e valor” | Conteúdo factual que precisa antes de checagem ou pesquisa |

---

## O que ela corrige

A skill separa o problema em cinco camadas. Essa divisão evita a revisão superficial, que só troca palavras, mas mantém a mesma estrutura robótica.

| Camada | O que procura | Exemplo de correção |
|---|---|---|
| Frases prontas | Aberturas, conectores, intensificadores e jargão | “É importante destacar que” vira começo direto |
| Estruturas | Contraste fabricado, falsa agência, passiva evasiva | “O mercado exige” vira quem exige e o quê |
| Ritmo | Tríades, punchline automática, fragmentos dramáticos | “Clareza. Consistência. Presença.” vira relação causal |
| Registro | Ajuste por canal e gênero textual | E-mail preserva cortesia; documentação preserva passiva útil |
| Exemplos | Modelos antes/depois | Guia prático para reescrita sem aplicar regra cega |

---

## Instalar

### Testar agora, sem instalar

Abra [`SKILL.md`](./SKILL.md), copie o conteúdo inteiro e cole numa conversa nova com seu modelo de IA. Em seguida, cole o texto que quer revisar e peça algo como:

```text
Use esta skill para revisar o texto abaixo. Quero diagnóstico curto e versão reescrita em PT-BR natural.

[cole o texto]
```

### Instalar no Claude Code / Cowork

```bash
SKILL=nem-parece-ia
mkdir -p ~/.claude/skills/$SKILL
curl -sL https://raw.githubusercontent.com/1marcelserrano/mscreative-skills/main/skills/$SKILL/SKILL.md \
  -o ~/.claude/skills/$SKILL/SKILL.md
```

Essa instalação rápida carrega apenas o arquivo principal. Para usar as referências completas, prefira copiar a pasta inteira.

### Instalar com referências completas

```bash
git clone https://github.com/1marcelserrano/mscreative-skills.git
cp -r mscreative-skills/skills/nem-parece-ia ~/.claude/skills/
```

Depois disso, reinicie a sessão do Claude. A skill dispara quando o pedido envolve revisão, reescrita, naturalização ou diagnóstico de texto em PT-BR.

---

## Como pedir

A skill entende pedidos naturais. Alguns exemplos:

```text
Revisa esse texto para não parecer IA.
```

```text
Tira o lero-lero corporativo e deixa mais direto, em PT-BR.
```

```text
Diagnostica o que está artificial nesse post e reescreve mantendo minha voz.
```

```text
Deixa esse e-mail mais natural, sem ficar seco ou agressivo.
```

```text
Reescreve essa landing page cortando abstração e promessa genérica.
```

---

## Estrutura

```text
nem-parece-ia/
├── SKILL.md
├── README.md
├── CHANGELOG.md
├── NOTICE.md
└── references/
    ├── atribuicao-e-uso.md
    ├── checklist.md
    ├── estruturas-ptbr.md
    ├── exemplos.md
    ├── formatacao-ptbr.md
    ├── frases-ptbr.md
    ├── hermetismo-ptbr.md
    ├── metaforas-ptbr.md
    ├── registros.md
    └── ritmo-ptbr.md
```

---

## Princípio editorial

> Cortar o que anuncia, inflama ou teatraliza. Preservar o que informa, situa, prova ou move o texto.

A skill não transforma tudo em texto seco. Ela calibra a edição por registro. Um e-mail pode manter cortesia. Um texto acadêmico pode manter cautela. Uma documentação técnica pode usar voz passiva. Um post pode aceitar frase curta, desde que ela não seja só pose.

---

## Atribuição

Esta skill é uma adaptação brasileira inspirada em [`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop). O projeto original é licenciado sob MIT. Esta versão recria a taxonomia, os exemplos e os critérios para português do Brasil, com foco em uso editorial responsável.

---

<sub>Forjado na [MSCREATIVE.SYSTEMS™](https://mscreative.systems) — Barcelona</sub>
