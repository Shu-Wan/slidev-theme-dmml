# Layouts

Every layout is a Vue component under `layouts/`. Select one per slide via the
`layout:` frontmatter key.

## `cover`

Title slide. Big title, subtitle, presenter, affiliation, date.

```yaml
---
layout: cover
eyebrow: DMML Lab · Spring 2026
title: Learning from Large-Scale Graphs
subtitle: Scalable methods for node classification under distribution shift
presenter: Jane Researcher
affiliation: Data Mining & Machine Learning Lab, ASU
date: April 17, 2026
---
```

## `intro`

Presenter introduction. Avatar, role, affiliation, and link chips.

```yaml
---
layout: intro
name: Jane Researcher
role: PhD Candidate, Computer Science
affiliation: ASU · DMML Lab
avatar: https://…/avatar.jpg
links:
  - { label: jane.asu.edu, url: https://asu.edu }
  - { label: '@jane-research', url: https://github.com }
---
Short bio in the slide body.
```

## `toc`

Auto-generated table of contents. Pulls every slide whose `layout: section`
(and whose `hideInToc` is not `true`), then renders its `num` + `title` +
`subtitle`.

```yaml
---
layout: toc
heading: Agenda
hideInToc: true
---
```

## `section`

Section divider. Maroon field, gold accent rule, big section number.

```yaml
---
layout: section
num: '01' # keep as a string so leading zeros survive YAML parsing
title: Motivation
subtitle: Why distribution shift breaks graph learning in practice.
part: Part 1 of 4
---
```

## `default`

Standard content. Markdown body renders as-is. Optional heading pulls a
maroon rule underneath.

```yaml
---
layout: default
heading: The setup
---

- bullet one
- bullet two

$$ \mathcal{L}(\theta) = \mathbb{E}[\ell(f_\theta(x), y)] $$
```

## `two-cols`

Two-column grid. `split` accepts any `grid-template-columns` value.

```yaml
---
layout: two-cols
heading: Message passing, in one slide
split: 1fr 1.2fr
---

::left::

Left column markdown.

::right::

Right column markdown.
```

## `image`

Image slide. `position: full` fills the stage; `left` / `right` puts the
image on that side and the markdown body on the other. `fill: true` covers
the image area; `false` fits.

```yaml
---
layout: image
image: https://…/figure.png
position: left
tag: Figure 1
title: Pipeline overview
alt: Diagram of the pipeline
---
Caption / discussion body here.
```

## `quote`

Large pull-quote with attribution.

```yaml
---
layout: quote
author: Judea Pearl
source: The Book of Why
---
A system that understands *why* is more useful than one that only predicts *what*.
```

## `end`

Closing slide. Maroon field, gold "Thank you", contact info.

```yaml
---
layout: end
thanks: Thank you.
subtitle: Questions, critiques, and collaborations welcome.
email: jane@asu.edu
website: dmml.asu.edu
github: '@jane-research'
date: April 17, 2026
---
```
