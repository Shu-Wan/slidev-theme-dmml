# Getting started

## Install

```bash
npm i -D slidev-theme-dmml
```

In your deck's frontmatter:

```yaml
---
theme: dmml
---
```

## Dev vs. build vs. export

Slidev gives you three very different commands. If you are new to Slidev, this is
the part that trips people up first.

### `slidev` (dev server)

```bash
npm run dev
```

- Starts a **Vite dev server** at `http://localhost:3030`.
- Hot-reloads on every edit to `example.md`, layouts, styles, or components.
- Opens the **presenter view** at `/presenter` (speaker notes, next-slide preview, timer).
- Use this while you are _writing the deck or iterating on the theme_.
- The dev server never writes a deployable artifact — nothing leaves memory.

### `slidev build` (static web deck)

```bash
npm run build
```

- Produces a **static SPA** in `dist/` (HTML + JS + CSS).
- Deploy `dist/` to Netlify, Vercel, GitHub Pages, or any static host.
- Viewers navigate with the arrow keys in a browser. Interactive features
  (click-through animations, embedded code, live components) all still work.
- Use this when you want people to _view the deck on the web_.

### `slidev export` (PDF / PNG / PPTX)

```bash
npm run export              # PDF (default)
npx slidev export --format png example.md
npx slidev export --format pptx example.md
```

- Uses **Playwright** under the hood to render every slide and pack the frames
  into a file. The first run will download a Chromium browser (~150 MB).
- Output is static — click-through steps collapse into one final frame per
  slide. For stepped animations, pass `--with-clicks`.
- Use this when you need to _hand the deck to someone offline_ (reviewers,
  conference submissions, archive copies).

### TL;DR

| Command  | Output              | When                         |
| -------- | ------------------- | ---------------------------- |
| `dev`    | live dev server     | writing / iterating          |
| `build`  | `dist/` static site | hosting on the web           |
| `export` | `slides-export.pdf` | offline / print / conference |

## Dark mode

Press `d` in any view to toggle. The ASU wordmark swaps to its white variant
and the Shiki code theme flips from `github-light` to `github-dark`. You can
also force a scheme in the deck's frontmatter:

```yaml
colorSchema: light # or "dark", or "both" (default — user choice)
```

## Fonts

The theme bundles Geist Variable and Geist Mono via `@fontsource-variable`, so
presentations render identically offline. No external font request is made.

## For theme authors: publishing

This repo _is_ the theme package. If you forked it to maintain your own
variant, here's how to release it.

### What ships to npm

`package.json` uses a `files` allowlist, so the published tarball contains
**only**:

- `layouts/`, `components/`, `styles/`, `setup/`, `assets/` — runtime
- `package.json`, `README.md`, `LICENSE`, `CHANGELOG.md` — metadata (first
  three are always included by npm regardless of `files`)

Everything else — `example.md`, `screenshots/`, `docs/`, `node_modules/`,
`dist/` — stays out. Verify before you publish:

```bash
npm pack --dry-run
```

### Release

1. Bump `version` in `package.json` (follow [semver](https://semver.org/)).
2. Add a matching entry to `CHANGELOG.md`.
3. Commit and tag:

   ```bash
   git commit -am "release: v0.2.0"
   git tag v0.2.0
   ```

4. Publish:

   ```bash
   npm login
   npm publish --access public
   ```

   The `prepublishOnly` script builds `example.md` as a smoke test — if any
   layout is broken, the publish aborts before the tarball is uploaded.

5. Push the tag: `git push && git push --tags`.

### Local testing before publish

To try the theme in a separate deck without publishing:

```bash
# In the theme repo
npm link

# In your deck
npm link slidev-theme-dmml
```

Or reference the directory directly in the deck's frontmatter:

```yaml
theme: ../path/to/slidev-theme-dmml
```
