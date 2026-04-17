# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
