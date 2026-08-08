<div align = "center">

# tinyGPT

[![Read My Paper](https://img.shields.io/badge/Read%20My%20Paper-View%20PDF-blue?style=for-the-badge&logo=readthedocs&logoColor=white)](https://shiiiivanshsingh.github.io/tinyGPT-research-paper/tinyGPT_ICDT2026.pdf)

[![Source Code](https://img.shields.io/badge/Source%20Code-tinyGPT-black?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ShiiiivanshSingh/tinyGPT)



[![Documentation](https://img.shields.io/badge/Documentation-tinyGPT-orange?style=for-the-badge&logo=gitbook&logoColor=white)](https://shiiiivanshsingh.github.io/tinyGPT/)
[![Detailed Results](https://img.shields.io/badge/Detailed%20Results-View-purple?style=for-the-badge&logo=chartdotjs&logoColor=white)](https://shiiiivanshsingh.github.io/tinyGPT/results/)
[![How It Works](https://img.shields.io/badge/How%20It%20Works-Documentaion-red?style=for-the-badge&logo=googlescholar&logoColor=white)](https://shiiiivanshsingh.github.io/tinyGPT/how-it-works/autograd/)


</div>

A character-level transformer implemented entirely from scratch in C++ — no ML libraries, no autograd framework, no BLAS. Every tensor op, backward rule, and the Adam optimizer are hand-derived on top of a self-built matrix autograd engine.

Two versions:
- **tinygpt** — single head, single block, no LayerNorm
- **tinygpt2** — 4 heads, 2 blocks, Pre-LayerNorm

Both trained on *Alice's Adventures in Wonderland* (~50 KB, 64 unique characters).



<div align = "center">

## Results

| Iter | tinygpt (8k) | tinygpt2 (10k) | tinygpt2 (20k) |
|------|-------------|-----------------|-----------------|
| 1000 | 2.44 | 2.43 | 2.43 |
| 5000 | 1.99 | 1.92 | 1.89 |
| 8000 | 1.77 | 1.64 | 1.64 |
| 10000 | — | 1.59 | 1.59 |
| 18800 | — | — | 1.34 (best) |
| 20000 | — | — | 1.40 |

</div>

For results and comparison bw multiple iterations [visit here](https://github.com/ShiiiivanshSingh/tinyGPT#loss-comparison-same-corpus-same-seed) or for more detailed insights and raw data [visit here.](https://shiiiivanshsingh.github.io/tinyGPT/results/)

tinygpt2's added multi-head attention and Pre-LayerNorm reduce final loss from 1.77 to 1.59 at comparable iteration counts, and to 1.40 with extended training. LayerNorm was deliberately omitted from tinygpt — it was implemented and verified correct via numerical gradient checking, but converged more slowly at the single-block scale.

## Paper

Full writeup: [`Reseach_Paper.pdf`](https://shiiiivanshsingh.github.io/tinyGPT-research-paper/tinyGPT_ICDT2026.pdf)) — covers the autograd engine, a reference-cycle memory bug in the backward closures, and the multi-head attention / LayerNorm backward derivations.
</div>

## Author

Shivansh Pratap Singh — GLBITM
`cse23308@glbitm.ac.in`
