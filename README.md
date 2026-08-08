# tinyGPT

A character-level transformer implemented entirely from scratch in C++ — no ML libraries, no autograd framework, no BLAS. Every tensor op, backward rule, and the Adam optimizer are hand-derived on top of a self-built matrix autograd engine.

Two versions:
- **tinygpt** — single head, single block, no LayerNorm
- **tinygpt2** — 4 heads, 2 blocks, Pre-LayerNorm

Both trained on *Alice's Adventures in Wonderland* (~50 KB, 64 unique characters).

## Results

| Iter | tinygpt (8k) | tinygpt2 (10k) | tinygpt2 (20k) |
|------|-------------|-----------------|-----------------|
| 1000 | 2.44 | 2.43 | 2.43 |
| 5000 | 1.99 | 1.92 | 1.89 |
| 8000 | 1.77 | 1.64 | 1.64 |
| 10000 | — | 1.59 | 1.59 |
| 18800 | — | — | 1.34 (best) |
| 20000 | — | — | 1.40 |

tinygpt2's added multi-head attention and Pre-LayerNorm reduce final loss from 1.77 to 1.59 at comparable iteration counts, and to 1.40 with extended training. LayerNorm was deliberately omitted from tinygpt — it was implemented and verified correct via numerical gradient checking, but converged more slowly at the single-block scale.

## Paper

Full writeup: [`tinyGPT_ICDT2026.pdf`](./tinyGPT_ICDT2026.pdf) — covers the autograd engine, a reference-cycle memory bug in the backward closures, and the multi-head attention / LayerNorm backward derivations.

## Author

Shivansh Pratap Singh — GLBITM
`cse23308@glbitm.ac.in`
