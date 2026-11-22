# orientador-chato-tcc

Skill para Claude que pesquisa referências acadêmicas reais, confere cada afirmação no
texto original da fonte e escreve trechos de TCC, monografia, artigo ou projeto de
pesquisa sem marcas de texto gerado por IA.

O nome vem do orientador que pede a página de cada citação e devolve o capítulo cheio de
"fonte?" na margem.

## O que ela faz

1. Pergunta o que falta saber sobre o trabalho (área, nível, norma, recorte).
2. Pesquisa em bases reconhecidas: SciELO, BDTD, Oasisbr, Portal de Periódicos CAPES,
   repositórios de universidades, Scopus, Web of Science, PubMed, IEEE Xplore, entre
   outras.
3. Abre cada publicação e anota afirmação + trecho + página. O que não foi encontrado na
   fonte não entra no texto.
4. Escreve seguindo regras contra marcas de texto gerado por IA e faz uma autoauditoria.
5. Envia o texto a dois agentes independentes:
   - **revisor de texto:** lê como a banca leria e aponta afirmações sem embasamento,
     incoerências, problemas de estrutura e vícios de linguagem;
   - **verificador de fontes:** reabre cada fonte por conta própria e confere metadados,
     DOI, retratação e se a afirmação diz o mesmo que a fonte.
6. Corrige o que os revisores apontaram e entrega o texto com referências, tabela de
   verificação e lista de pendências.

Pedidos menores rodam só parte do fluxo: "ache referências sobre X" para depois da
verificação e entrega a lista conferida; "confira esta citação" usa só o verificador de
fontes.

## Estrutura

```
skills/orientador-chato-tcc/
├── SKILL.md                  fluxo principal
└── references/
    ├── fontes.md             bases, repositórios e critérios de credibilidade
    ├── verificacao.md        protocolo de verificação das fontes
    ├── sinais-ia.md          como escrever e padrões de IA a evitar
    ├── agentes.md            instruções dos dois agentes revisores
    └── abnt.md               citações (NBR 10520:2023) e referências (NBR 6023:2018)
```

## Instalação

Claude Code: copie a pasta `skills/orientador-chato-tcc` para `~/.claude/skills/`.

Outros clientes que aceitam skills: compacte a pasta `orientador-chato-tcc` em `.zip` e
envie pela área de skills do aplicativo.

A revisão por agentes usa a ferramenta de subagentes quando ela existe. Sem ela, a skill
faz as duas revisões em passagens separadas e avisa que a revisão não foi independente.

## Limitações

- Artigos atrás de paywall ou em sites que bloqueiam acesso automatizado não podem ser
  lidos. Nesses casos a skill pede o PDF em vez de deduzir o conteúdo.
- A skill reduz, mas não elimina, o risco de erro. Confira as referências antes de
  entregar o trabalho.
- Verifique a política da sua instituição sobre uso de IA em trabalhos acadêmicos.

## Créditos

- Padrões de escrita baseados em
  [Wikipédia:Sinais de texto gerado por inteligência artificial](https://pt.wikipedia.org/wiki/Wikip%C3%A9dia:Sinais_de_texto_gerado_por_intelig%C3%AAncia_artificial)
  (CC BY-SA 4.0), traduzida e adaptada de
  [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing).
- Lista de expressões em português inspirada na
  [adaptação para o português](https://ofelipemart.substack.com/p/a-skill-que-tira-a-cara-de-ia-do)
  do humanizer, de Siqi Chen (licença MIT), publicada por Felipe Mart.
- Estrutura de skill com `references/` carregadas sob demanda inspirada em
  [David-Saeteros/claude-skills](https://github.com/David-Saeteros/claude-skills).

## Autor

[Syneers](https://github.com/Syneers) · repositório: [Syneers/orientador-chato-tcc](https://github.com/Syneers/orientador-chato-tcc)
