# Registro — as outras frentes

## Tipografia (clamp)
| Título | Regra | ~360px | ~1280px |
|---|---|---|---|
| `h1` (vitrine e página do local) | `clamp(1.75rem, 1.25rem + 2.2vw, 2.5rem)` | 20 + 0,022×360 = 27,9px → piso **28px** | 20 + 0,022×1280 = 48,2px → teto **40px** |
| `.hero h2` (vitrine) | `clamp(1.5rem, 1.1rem + 1.8vw, 2rem)` | 17,6 + 0,018×360 = 24,1px → **~24px** | 17,6 + 0,018×1280 = 40,6px → teto **32px** |

O `h1` atinge o teto em ~909px; o `h2`, em ~800px. Removi os `font-size` fixos do `@media (min-width: 48em)` para não anularem o `clamp`.

## Mídia
- Regra universal `img, picture, svg, video { max-width: 100%; height: auto }`.
- `object-fit: cover` + `aspect-ratio` (16/9 nos cards, 16/10 na ilustração da detalhe): a caixa mantém a proporção mesmo com imagem de outro tamanho.
- `width`/`height` adicionados nas `<img>` para reservar espaço antes do carregamento.

## Usuário
- Meta viewport: já estava nas duas páginas.
- Área de toque: `min-height: 44px` nos menus (principal, categorias, rodapé, interno), botão "Ver locais e eventos" e lista de links.
- Foco: `a:focus-visible` virou `:focus-visible` (vale para qualquer elemento interativo futuro).

## Auditoria (Lighthouse → Acessibilidade)
Não consigo rodar o Lighthouse aqui: **rode em `index.html` e `detalhe.html` e anote a nota real**. Pontos que li no código e que podem aparecer no relatório:
- Contraste: calculei os pares principais (texto/fundo, links, tag, botão) e todos passam de 4,5:1; confirme no relatório.
- `href="#"` (Localização, Instagram, Sugerir correção, CCXP, categorias): links sem destino real; não derrubam a nota, mas são pendência de conteúdo.
- Links repetidos "Ver detalhes →" nos dois cards: texto igual para destinos diferentes; se o Lighthouse apontar, use `aria-label` com o nome do evento.
- Corrigi por conta própria: o CSS se chamava `style (2).css` (espaço no nome); virou `style.css` e os dois `<link>` foram atualizados.


## Por página: folha única × correção própria
| Página | A folha única resolveu sozinha | Precisou de correção própria |
|---|---|---|
| `index.html` | `clamp` do `h1`, regra de imagem, foco, alvos de toque nos menus e no botão | `.hero h2` (só existe na vitrine); `object-fit`/`aspect-ratio` nas imagens dos cards; `width`/`height` nas `<img>`; `href` do CCXP ainda `#` |
| `detalhe.html` | `clamp` do `h1`, regra de imagem, foco, alvos de toque (menu, barra interna, rodapé) | `aspect-ratio`/`object-fit` na `.park-illustration`; `width`/`height` da imagem; alvos de toque da `.link-list`; `href="#"` nos links de contato |
