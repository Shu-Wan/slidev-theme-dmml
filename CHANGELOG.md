# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.2] — 2026-04-17

### Fixed

- README gallery — corrected screenshot filenames (`09-end.png` → `10-end.png`, `10-cover-dark.png` → `11-cover-dark.png`, `11-section-dark.png` → `12-section-dark.png`) so the images render on the npm/GitHub README.
- Added `09-references.png` and `05b-cite-tooltip.png` to the gallery.

## [0.1.1] — 2026-04-17

### Fixed

- Corrected GitHub username in `homepage`, `repository`, and `bugs` URLs in `package.json` (`Shu` → `Shu-Wan`).

## [0.1.0] — 2026-04-17

### Added

- Initial theme release.
- Nine layouts: `cover`, `intro`, `toc`, `section`, `default`, `two-cols`, `image`, `quote`, `end`.
- Shared `Footer`, `DmmlLogo`, `AsuWordmark` components.
- Light and dark color schemes driven by CSS variables (`html.dark` / `html:not(.dark)`).
- ASU palette: maroon `#8C1D40`, gold `#FFC627`, full neutral scale.
- Geist Variable + Geist Mono typography via `@fontsource-variable`.
- Shiki syntax highlighting (`github-light` / `github-dark`) with maroon line-highlight.
- KaTeX LaTeX support (inherited from Slidev).
- `example.md` demo deck covering every layout.
- DMML monogram redrawn as inline SVG with `currentColor` fill.
