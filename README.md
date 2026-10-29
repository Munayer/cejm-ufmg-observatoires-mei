# Observatório do Microempreendedor Individual — MEI

**`site/index.html` é o produto.** Um único arquivo, com CSS e JS
embutidos, sem passo de build e sem dependência de rede: os gráficos são
SVG desenhado pelo próprio arquivo, então tudo abre offline. Serve em
qualquer host estático.

*Observatório do Microempreendedor Individual – MEI: reflexões sobre seus
números* é a pesquisa do Eixo 3 (Comércio, Consumo e Governança
Corporativa) do Centro de Excelência Jean Monnet da UFMG. O site é a
versão digital do relatório final; todo número nele vem desse documento.

Este repositório segue a estrutura do Observatório de Direitos Humanos
(`cejm-ufmg-observatoires-humanrights`): só `site/` vai para o ar; o resto
é documentação. A página partiu do protótipo `Observatorio_MEI.html`. O
repositório principal fica no
[Codeberg](https://codeberg.org/Munayer/cejm-ufmg-observatoires-mei), com
espelho no [GitHub](https://github.com/Munayer/cejm-ufmg-observatoires-mei).

## O que tem em `index.html`

- **Quem somos** — capa com o número de MEIs ativos (Portal do MEI,
  31 ago. 2026), quatro destaques do relatório, apresentação do
  observatório, equipe e as três lentes do método (revisão bibliográfica,
  análise normativa, dados secundários).
- **Relatórios** — os sete capítulos do relatório final em leitura
  digital, com sumário lateral (horizontal no celular) e a ressalva de
  comparabilidade entre as bases.
- **Gráficos** — sete indicadores tirados das tabelas do relatório (sexo,
  regiões, participação feminina por atividade, raça ou cor, raça e
  situação da atividade, escolaridade por sexo, necessidade e renda). O
  leitor escolhe dois recortes e vê a diferença; cada indicador mostra a
  fonte e uma nota de método.
- **Rodapé** — emblema "Cofinanciado pela União Europeia" e o aviso da
  EACEA, seguindo as orientações da Comissão Europeia para quem recebe
  financiamento da UE (as Ações Jean Monnet são do programa Erasmus+).

## Estrutura do repositório

```
site/index.html                       -- o produto. Editar direto; não há passo de build.
site/assets/eu/co-funded-pt-neg.png   -- emblema oficial da UE, versão para fundo escuro, sem alteração
site/_headers                         -- cabeçalhos HTTP (formato Netlify, lido pelo Codeberg Pages)
site/_redirects                       -- www → domínio principal (comentado até o domínio existir)
.claude/launch.json                   -- servidor local para o navegador do Claude Code
CLAUDE.md                             -- notas para sessões do Claude Code
README.md                             -- este arquivo
```

## Ver localmente

```
python -m http.server 8010 --directory site     # http://localhost:8010
```

Ou abrir `site/index.html` direto no navegador.

## Fonte

Relatório final da pesquisa, versão corrigida (arquivo
`2026 09 08_Observatório MEI - Relatório final (versão corrigida).pdf`).
Bases usadas por ele: Portal do Empreendedor, Mapa de Empresas, IBGE
(ano-base 2022) e Pesquisa Perfil MEI 2024 do Sebrae. O PDF fica fora do
repositório até se decidir publicá-lo.

## Pendente

- Publicar o site: enviar o ramo `pages` ao Codeberg (comando em
  `CLAUDE.md`).
- Domínio, e com ele a regra de `site/_redirects`.
- Licença (o Observatório de Direitos Humanos pretende AGPL-3.0-or-later).
- Publicar ou não o PDF do relatório (por exemplo, para download na aba
  Relatórios).
