---
theme: ./
colorSchema: auto
info: |
  A demo deck showcasing slidev-theme-dmml.
  Arizona State University · Data Mining & Machine Learning Lab.
highlighter: shiki
lineNumbers: true
drawings:
  persist: false
transition: fade
mdc: true
addons:
  - slidev-addon-citations
biblio:
  filename: refs.bib
  tooltips: true
  footnotes: short
  show_id: false
layout: cover
eyebrow: DMML Lab · Spring 2026
title: Learning from Large-Scale Graphs
subtitle: Scalable methods for node classification under distribution shift
presenter: Sparky the Sun Devil
affiliation: Data Mining & Machine Learning Lab, ASU
date: April 17, 2026
---

---
layout: intro
name: Sparky the Sun Devil
role: Mascot-in-Residence · Honorary PI
affiliation: ASU · Data Mining & Machine Learning Lab
avatar: https://upload.wikimedia.org/wikipedia/commons/thumb/9/99/Sparky_on_the_Field.jpg/250px-Sparky_on_the_Field.jpg
links:
  - { label: asu.edu, url: https://asu.edu }
  - { label: '@sparky', url: https://github.com }
  - { label: scholar profile, url: https://scholar.google.com }
---

My research lives at the intersection of **graph neural networks**, **robustness under distribution shift**, and the practical systems that keep them running at scale.

---
layout: toc
heading: Agenda
columns: 1
maxDepth: 1
hideInToc: true
---

---
layout: section
num: '01'
title: Motivation
subtitle: Why distribution shift breaks graph learning in practice.
part: Part 1 of 4
---

---
layout: default
heading: The setup
---

Modern graph learning systems face three recurring problems:

- **Shift**: training and deployment graphs rarely share a distribution.
- **Scale**: billion-edge graphs don't fit in one GPU.
- **Signal**: labels are expensive and sparse where they matter.

A concise framing: we want $\hat{y} = f_\theta(G, x)$ to minimize

$$
\mathcal{L}(\theta) = \mathbb{E}_{(G, x, y) \sim \mathcal{D}_{\text{test}}} \left[ \ell\!\left(f_\theta(G, x),\, y\right) \right]
$$

even when $\mathcal{D}_{\text{train}} \neq \mathcal{D}_{\text{test}}$.

---
layout: two-cols
heading: Message passing, in one slide
split: 1fr 1.2fr
---

::left::

For a node $v$ at layer $\ell$:

$$
h_v^{(\ell)} = \sigma\!\left( W^{(\ell)} \cdot \text{AGG}\!\left(\{h_u^{(\ell-1)} : u \in \mathcal{N}(v)\}\right) \right)
$$

- AGG: mean, sum, attention, … <Cite bref="kipf2017gcn" /><Cite bref="hamilton2017graphsage" />
- Depth $L$ controls receptive field.
- Robustness: depends on AGG + graph topology.

::right::

```python {all|1-3|5-11|all}
import torch
import torch.nn.functional as F
from torch_geometric.nn import GCNConv

class GCN(torch.nn.Module):
    def __init__(self, in_dim, hidden, out_dim):
        super().__init__()
        self.c1 = GCNConv(in_dim, hidden)
        self.c2 = GCNConv(hidden, out_dim)

    def forward(self, x, edge_index):
        x = F.relu(self.c1(x, edge_index))
        return self.c2(x, edge_index)
```

---
layout: quote
author: Judea Pearl
source: The Book of Why
---

A system that understands _why_ is more useful than one that only predicts _what_.

---
layout: section
num: '02'
title: Method
subtitle: A lightweight, causal re-weighting step on top of any GNN backbone.
part: Part 2 of 4
---

---
layout: image
image: https://images.unsplash.com/photo-1617791160536-598cf32026fb?w=1600
position: left
tag: Figure 1
title: Pipeline overview
alt: Diagram of the pipeline
---

Inputs flow left-to-right: we re-weight the training distribution with an inverse-propensity estimator, run standard GNN training, then apply a lightweight test-time adaptation step.

- `w_i = 1 / P(G_i ∈ train)` — estimated by a domain classifier.
- End-to-end: ~6% runtime overhead.

---
layout: default
heading: Results
---

| Dataset       | Baseline |     Ours | $\Delta$ |
| ------------- | -------: | -------: | -------: |
| ogbn-arxiv    |     70.2 | **72.1** |     +1.9 |
| ogbn-products |     76.4 | **78.8** |     +2.4 |
| Reddit-S      |     64.0 | **67.3** |     +3.3 |

Gains concentrate where the train/test shift is largest — consistent with our hypothesis. Datasets follow the Open Graph Benchmark protocol <Cite bref="hu2020ogb" />.

---
layout: section
num: '03'
title: Discussion
subtitle: Where this works, where it doesn't, and what's next.
part: Part 3 of 4
---

---
layout: default
heading: Limitations
---

- **Propensity estimation is fragile** when the domain classifier is over-confident.
- **No causal guarantees** beyond covariate shift; label shift is open.
- **Compute**: training cost is fine; eval cost rises with adaptation length.

---
layout: default
heading: References
---

<BiblioList :show-full-bib="true" />

---
layout: end
thanks: Thank you.
subtitle: Questions, critiques, and collaborations welcome.
email: sparky@asu.edu
website: dmml.asu.edu
github: '@sparky'
date: April 17, 2026
---
