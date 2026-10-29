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

Publicado pelo Codeberg Pages em `https://observatoriomeu.com` (www
redireciona para o domínio principal, ver `site/_redirects`; cabeçalhos em
`site/_headers`). O ramo `pages` do Codeberg contém só o conteúdo de
`site/`.

- Repositório principal: `codeberg.org/Munayer/cejm-ufmg-observatoires-mei`
  (remoto `codeberg`). O GitHub (`origin`) é espelho: recebe o mesmo `main`.
- Dois webhooks do Codeberg (domínio principal e www, filtro `pages`)
  publicam a cada push no ramo `pages`. A autorização está nos registros
  TXT `_git-pages-repository` na Hostinger, onde fica o DNS do domínio.
- O domínio se escreve com "meu", não "mei": é o nome registrado. Não
  corrigir.

## Comandos

Não há build, linter nem testes. Para ver o site localmente:

```
python -m http.server 8010 --directory site     # http://localhost:8010
```

(`.claude/launch.json` tem a mesma configuração, para o navegador do app.)

Para publicar (depois do commit em `main`), o ramo `pages` do Codeberg
recebe só o conteúdo de `site/` (mesmo fluxo do Observatório de Direitos
Humanos):

```
git push codeberg main "$(git subtree split --prefix=site HEAD):refs/heads/pages"
git push origin main
```

O `subtree split` é determinístico: sem mudança em `site/`, o ramo `pages`
não muda e nada é republicado. Deste PC, o envio ao Codeberg vai por SSH,
com a chave de implantação (ver `C:\bmm\sync\dev-github\CLAUDE.md`).

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
- Rodapé: emblema "Cofinanciado pela União Europeia" e marca do Centro
  de Excelência Jean Monnet, ambos na versão para fundo escuro, e o aviso
  da EACEA, como no Observatório SOMA. O emblema vai sem alteração e com
  pelo menos 1 cm de altura; a marca do CEJM fica ao lado, na mesma
  altura e nunca maior que o emblema (regra da UE para marcas exibidas
  com ele). `assets/cejm/cejm-pt-neg.png` é o logo branco do pacote do
  centro, recortado nas bordas transparentes e reduzido a 168 px de
  altura (3× os 56 px).

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
