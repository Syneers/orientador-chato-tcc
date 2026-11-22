---
name: orientador-chato-tcc
description: Pesquisa referências acadêmicas reais, confere cada afirmação no texto original da fonte e escreve trechos de TCC, monografia, artigo ou projeto de pesquisa sem marcas de texto gerado por IA, com revisão final por dois agentes independentes. Use para revisão bibliográfica, fundamentação teórica, introdução, estado da arte, "ache referências sobre X" ou "confira esta citação".
---

# Orientador chato (TCC)

Esta skill pesquisa referências acadêmicas reais, abre cada publicação para conferir se
o que será afirmado consta nela e escreve o texto acadêmico. Depois da escrita, o texto
passa por dois agentes independentes: um revisa estrutura e linguagem, o outro revalida
as fontes. Só então o texto é entregue.

## Arquivos de apoio

Leia cada arquivo quando chegar à etapa correspondente:

| Arquivo | Quando ler |
|---|---|
| `references/fontes.md` | etapa 2, antes de pesquisar |
| `references/verificacao.md` | etapa 3, antes de verificar a primeira fonte |
| `references/sinais-ia.md` | etapa 4, antes de escrever e de novo na autoauditoria |
| `references/agentes.md` | etapa 5, para montar as instruções dos revisores |
| `references/abnt.md` | etapas 4 e 7, ao formatar citações e referências |

## Fluxo

1. Levantar o que falta saber sobre o trabalho.
2. Pesquisar fontes.
3. Verificar cada fonte e anotar afirmação + trecho + página (ou seção).
4. Escrever e auditar o próprio rascunho.
5. Enviar o texto aos dois agentes revisores, em paralelo.
6. Consolidar os pareceres e corrigir.
7. Entregar.

Dentro do modo escolhido, não pule etapas. Não escreva antes de ter as anotações
verificadas.

### Modos

O pedido define quais etapas rodam:

| Pedido | Etapas | Entrega |
|---|---|---|
| Escrever ou reescrever trecho do trabalho | 1 a 7 | completa |
| "Ache referências sobre X" | 1 a 3 | itens 2, 3 e 5 da etapa 7 |
| "Confira esta citação" ou as citações de um texto do usuário | 3, com o modelo do Agente 2 | itens 3 e 5, mais o que a fonte diz de fato em cada divergência |

No modo de conferência, não reescreva o texto do usuário sem que ele peça.

## 1. Antes de pesquisar

Pergunte apenas o que não estiver claro e não puder ser deduzido do pedido:

- área e tema;
- nível (graduação, especialização, mestrado, doutorado);
- norma (ABNT, salvo indicação contrária; não pergunte);
- idioma das fontes aceitas e recorte temporal;
- extensão e seção do trabalho;
- opcional: uma amostra de texto do próprio usuário, para imitar a voz dele.

## 2. Pesquisa

Siga `references/fontes.md`. Em resumo: use os agregadores para achar publicações
(OpenAlex, Crossref, Semantic Scholar, Google Acadêmico, Portal de Periódicos CAPES),
priorize fontes com revisão por pares e indexação reconhecida, e nunca cite Wikipédia,
blogs ou sites de resumos. Nunca contorne CAPTCHA, login ou paywall.

## 3. Verificação

Siga `references/verificacao.md`. Regras que valem sempre, mesmo sem abrir o arquivo:

- Só cite o que você abriu e leu. Cada afirmação atribuída a uma fonte precisa de
  trecho + página (ou seção, em documento sem paginação) anotados.
- Sem trecho que a sustente, a afirmação não entra no texto.
- Nunca invente referência, autor, DOI, página, número ou dado.
- Se só o resumo estiver acessível, a fonte só sustenta o que está escrito no resumo.
- Paywall ou bloqueio: procure versão em acesso aberto; se não houver, use o resumo
  dentro do limite acima e peça o PDF ao usuário para o que for além dele. Não deduza
  conteúdo pelo título. Continue com as demais fontes enquanto o PDF não chega.
- Status de cada referência: VERIFICADA, VERIFICADA PELO RESUMO, NÃO VERIFICADA ou
  DESCARTADA. Só as duas primeiras entram no texto.

Análise própria (comparar fontes, avaliar métodos, apontar lacuna) não precisa de
citação, desde que decorra das fontes citadas. Lacuna só se declara dentro do recorte
pesquisado: "nas bases consultadas, não foi encontrado estudo que...", nunca "nenhum
estudo analisou...".

## 4. Escrita

Leia `references/sinais-ia.md` antes de escrever.

Princípio: trocar palavra por sinônimo não resolve. Um texto ganha cara de IA mais pela
estrutura do que pelo vocabulário: parágrafos do mesmo tamanho, todos fechando com
frase-síntese, autores apresentados um por vez sem diálogo, ideias genéricas no lugar de
dados.

Voz do autor: se o usuário enviou um texto dele, reproduza tamanho médio das frases,
pessoa verbal, conectivos, grau de formalidade e forma de introduzir citações. Não
"corrija" o estilo dele para um padrão genérico. Sem amostra, use registro acadêmico
neutro. Se a amostra usa um padrão da lista de `sinais-ia.md`, ele pode aparecer no
texto, mas nunca com frequência maior que na amostra; os demais itens da lista valem
normalmente.

Autoauditoria, obrigatória antes da etapa 5:

1. Rascunhe só com as anotações verificadas.
2. Percorra o rascunho item por item da lista de `references/sinais-ia.md`: procure cada
   expressão, conte conectivos, compare o tamanho dos parágrafos, veja como cada um
   termina.
3. Reescreva cada ocorrência reconstruindo a frase, não trocando por sinônimo.
4. Confira se a reescrita não mudou o que a fonte diz.

## 5. Revisão por dois agentes

Com o rascunho auditado, dispare os dois agentes em paralelo com a ferramenta de
subagentes (Agent ou Task). Use agentes novos, de uso geral, com acesso à web. Não use
fork: o revisor não pode herdar o raciocínio de quem escreveu.

Cada agente começa sem contexto. Copie o modelo de instruções de `references/agentes.md`
na íntegra, preencha os campos entre chaves e envie. Não resuma o modelo.

- **Agente 1, revisor de texto:** recebe só o texto (parágrafos numerados), área, nível
  e norma. Aponta afirmações sem embasamento, incoerências no texto inteiro, problemas de
  estrutura acadêmica, marcas de IA e vícios de linguagem.
- **Agente 2, verificador de fontes:** recebe texto, referências, tabela de verificação
  e o caminho dos PDFs enviados pelo usuário. Reabre cada fonte por conta própria e não
  aceita a tabela como prova.

Sem ferramenta de subagentes: faça as duas revisões em passagens separadas, seguindo os
mesmos modelos, reabrindo as fontes em vez de consultar suas anotações. Avise na entrega
que a revisão não foi independente.

## 6. Consolidação

- CRÍTICO: corrija. Só mantenha o trecho se tiver evidência contrária (trecho e página
  da fonte); nesse caso, registre o motivo na entrega e liste o ponto nas pendências.
- IMPORTANTE: corrija, ou mantenha registrando o motivo na entrega.
- MENOR: corrija quando a mudança não alterar o que a fonte diz; senão, ignore.
- Afirmação sem embasamento apontada pelo Agente 1: busque fonte (passando pela etapa 3),
  atenue ou corte. Não deixe afirmação forte sem fonte.
- Agente 2:
  - DIVERGENTE ou RETRATADA: corrija a afirmação para o que a fonte diz, troque a fonte
    ou retire a citação.
  - METADADOS ERRADOS: corrija a referência pela página oficial.
  - NÃO ACESSÍVEL em fonte que você marcou VERIFICADA com trecho e página: mantenha,
    anote "não revalidada pelo Agente 2" na tabela e liste nas pendências. Sem trecho e
    página anotados, trate como DIVERGENTE.
- Trechos com fonte nova ou afirmação alterada voltam ao Agente 2 uma única vez (segunda
  rodada); o que restar vai para as pendências.
- Refaça a autoauditoria nos trechos reescritos.

## 7. Entrega

1. Texto final, sem a numeração de parágrafos usada na revisão.
2. Referências na norma escolhida, só VERIFICADAS e VERIFICADAS PELO RESUMO (modelos em
   `references/abnt.md`).
3. Tabela de verificação: referência | status | DOI/link | afirmação usada | trecho e
   página | resultado do Agente 2.
4. Apontamentos dos revisores e o que foi feito com cada um (corrigido, cortado, mantido
   e por quê).
5. Pendências: afirmações sem fonte encontrada, fontes que não puderam ser abertas ou
   revalidadas e PDFs que o usuário precisa enviar.

Comentários para o usuário ficam nesta seção, nunca misturados ao texto acadêmico.

## Coisas a evitar

- Escrever antes de ter as anotações verificadas.
- Citar fonte que não foi aberta.
- Usar a tabela de verificação como prova na revisão de fontes.
- Passar o raciocínio da escrita para os revisores (sem fork).
- Resolver apontamento trocando palavra por sinônimo.
- Manter um CRÍTICO sem evidência contrária, ou mantê-lo sem listá-lo nas pendências.
