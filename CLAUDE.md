# CLAUDE.md

Notas para sessões do Claude Code neste repositório. As regras gerais da
pasta de desenvolvimento estão em `C:\bmm\sync\dev-github\CLAUDE.md`; o que
segue é específico deste projeto.

## O que é

Observatório do Microempreendedor Individual (MEI), pesquisa do Eixo 3 do
Centro de Excelência Jean Monnet da UFMG. **`site/index.html` é o
produto**: um único arquivo com CSS e JS embutidos, sem passo de build e
sem rede. O resto do repositório é documentação. Ver `README.md` para o
conteúdo da página.

Ainda não publicado: o git é só local, sem remoto. Falta criar o
repositório (Codeberg como principal, GitHub como espelho, como no
Observatório de Direitos Humanos) e definir o domínio.

## Comandos

Não há build, linter nem testes. Para ver o site localmente:

```
python -m http.server 8010 --directory site     # http://localhost:8010
```

(`.claude/launch.json` tem a mesma configuração, para o navegador do app.)

Para publicar, quando o repositório e o Codeberg Pages existirem (mesmo
fluxo do Observatório de Direitos Humanos):

```
git push codeberg main "$(git subtree split --prefix=site HEAD):refs/heads/pages"
git push origin main
```

## Estrutura de `index.html`

- `<style>` numa linha só, no topo; paleta em `:root` (`--ink`, `--paper`,
  `--green`, `--mint`, `--gold`, `--coral`). As regras de tela estreita
  (`max-width:800px` e `480px`) ficam no fim da folha.
- Três abas (`role="tab"`, `data-tab`): `#sobre` (Quem somos),
  `#relatorios` (Relatórios), `#graficos` (Gráficos). A aba aberta vai
  para o fragmento da URL, e `index.html#graficos` abre direto nela.
- Relatórios: capítulos `section#r-*`, numerados em `.chapter`. Um
  capítulo novo entra também no sumário `.report-index`
  (`data-scroll="r-…"`).
- Gráficos: o objeto `datasets` no `<script>` do fim. Cada indicador tem
  `title`, `subtitle`, `source`, `unit`, `decimals`, `note` e `items`
  (`[rótulo, valor]`). O gráfico de barras é SVG desenhado por `draw()`,
  sem biblioteca; as cores das barras estão repetidas ali, então mudar a
  paleta exige mudar `draw()` também.
- Rodapé: emblema "Cofinanciado pela União Europeia" (versão negativa,
  para o fundo escuro) e o aviso da EACEA, iguais aos do Observatório
  SOMA. O emblema vai sem alteração e com pelo menos 1 cm de altura.

## Regras de conteúdo

- **Todo número vem do relatório final**, com fonte e nota no indicador;
  nada é inventado nem arredondado de novo sem dizer. O relatório está em
  `C:\bmm\sync\2026 09 08_Observatório MEI - Relatório final (versão corrigida).pdf`
  e fica fora do git (`*.pdf` no `.gitignore`) até a decisão de
  publicá-lo. Para conferir um número:
  `pdftotext -layout "<relatório>.pdf" - | grep -F "96,63"`.
- Bases com universos e datas diferentes (Portal do Empreendedor, IBGE
  2022, Sebrae 2024) não se comparam como se fossem uma só; a ressalva de
  comparabilidade fica visível.
- `<blockquote>` só para trecho que existe no relatório, copiado sem
  mudança, dentro de `<figure>` com a página em `<figcaption>`
  ("Relatório final, p. 28").

## Convenções

- Texto do site, documentação e mensagens de commit em **português**,
  título no imperativo, corpo com o que mudou e por quê.
- Licença: a definir.
