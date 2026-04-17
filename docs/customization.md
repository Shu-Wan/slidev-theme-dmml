# Customization

The theme is driven by CSS variables, so most visual tweaks can be made
without forking the layouts. Add an `style.css` (or any file imported from
your deck's `setup/`) and override the tokens you want.

## Color tokens

Defined in `styles/layout.css` under `html:not(.dark)` and `html.dark`:

```css
:root {
  --dmml-maroon: #8c1d40;
  --dmml-maroon-bright: #b2355e; /* dark-mode accent */
  --dmml-gold: #ffc627;

  --dmml-bg: #ffffff;
  --dmml-fg: #0f0f10;
  --dmml-muted: #5a5a5e;
  --dmml-rule: rgba(0, 0, 0, 0.08);

  --slidev-theme-primary: var(--dmml-maroon);
}

html.dark {
  --dmml-bg: #0f0f10;
  --dmml-fg: #f2f2f3;
  --dmml-muted: #9a9a9e;
  --dmml-rule: rgba(255, 255, 255, 0.08);
  --slidev-theme-primary: var(--dmml-maroon-bright);
}
```

To re-theme, override in your own stylesheet:

```css
:root {
  --dmml-maroon: #7a1833;
}
html.dark {
  --dmml-maroon-bright: #c0476e;
}
```

## Fonts

The theme ships Geist and Geist Mono via `@fontsource-variable`. To use a
different face, set `fonts` in your deck's frontmatter and Slidev will load
it for you:

```yaml
---
theme: dmml
fonts:
  sans: Inter
  mono: JetBrains Mono
---
```

## Footer

Every non-cover, non-section, non-end layout uses `components/Footer.vue`. It
shows the ASU wordmark (left), current slide title (center), and
`currentPage / total` + DMML monogram (right). To hide it on a specific
slide, add `hideFooter: true` to that slide's frontmatter and the layout
will skip it (see `layouts/default.vue` for how the flag is read).

## Logos

- `components/DmmlLogo.vue` — renders `assets/dmml-logo.png` as a CSS
  `mask-image` with `background-color: currentColor`, so the monogram
  inherits the surrounding text color and adapts to light/dark mode without
  shipping two PNGs.
- `components/AsuWordmark.vue` — switches between the maroon and white PNGs
  in `assets/` via a `MutationObserver` on `html.classList`.

To drop in your own lab monogram, replace `assets/dmml-logo.png` with a PNG
that has a transparent background and opaque black shapes — the mask trick
handles colorization automatically.

## Citations (BibTeX)

Citation rendering is handled by the `slidev-addon-citations` addon. The
theme ships styling that matches the ASU palette — install the addon and
cite as normal:

```bash
npm i -D slidev-addon-citations
```

```yaml
---
theme: dmml
addons:
  - slidev-addon-citations
biblio:
  filename: refs.bib
---
```

Drop the `.bib` file at `public/biblio/refs.bib` in your deck. Then:

- Inline: `<Cite bref="kipf2017gcn" />` renders a small maroon chip.
- References slide: `<BiblioList :show-full-bib="true" />` prints every
  entry from the bib file. Without `show-full-bib`, only entries already
  cited on prior slides show up — which means the bibliography is empty if
  the viewer jumps straight to that slide.

Styled class hooks (override in your own stylesheet if needed):

| Class            | What it is                           |
|------------------|--------------------------------------|
| `.biblio_ref`    | Inline citation chip (no tooltip)    |
| `.biblio_tooltips` | Inline chip with hover tooltip     |
| `.biblio_graphy` | Wrapper for `<BiblioList />`         |
| `.biblio_list`   | The `<ul>`                           |
| `.biblio_line`   | Each `<li>` entry                    |
| `.biblio_id`     | The `[1]` identifier                 |
| `.biblio_fullref`| The full reference text              |
| `.biblio_pageref`| Back-links to cited-on pages         |
