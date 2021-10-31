---
title: "Style Tests"
date: 2021-10-31
math: true
draft: true
---

A little playground for testing out style changes.

---

Before block quote.

> This is meant to be a fairly long quote to try to force a line wrap within a block quote. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt.
> Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem. Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam, nisi ut aliquid ex ea commodi consequatur? Quis autem vel eum iure reprehenderit qui in ea voluptate velit esse quam nihil molestiae consequatur, vel illum qui dolorem eum fugiat quo voluptas nulla pariatur?

End block quote.

---

A quick test of inline math: $F(g) = \frac{3 \times (1 - g^2)}{2 \times (2 + g^2)}$ is one half of a phase function. An equation on a standalone line looks like this:

$$t(P_aP_b, \lambda) = 4\pi \times K(\lambda) \times \int_{P_a}^{P_b}exp\left(\frac{-h}{H_0}\right) ds$$

However, it doesn't play nice with footnotes. Neither

$$\lambda(x) = \Gamma(x^\prime - 1)$$[^1]

nor

$$\lambda(x) = \Gamma(x^\prime - 1)[^1]$$

are desirable.

[^1]: [GPU Gems 2, Chapter 16 - Accurate Atmospheric Scattering](https://developer.nvidia.com/gpugems/gpugems2/part-ii-shading-lighting-and-shadows/chapter-16-accurate-atmospheric-scattering)

---

|      | X | Y | Z | x | y |
|------|:-:|:-:|:-:|:-:|:-:|
| Red  | 2 | 123 | 23.4 | 39.2 | 1.2 |
| Blue | $\lambda^4$ | Hello | 99 | `asdf` | $F(x) = x$ |

However, the table does a weird y-overflow thing with some taller $\KaTeX$ outputs:

|      | X | Y | Z | x | y |
|------|:-:|:-:|:-:|:-:|:-:|
| Red  | 2 | $\int_{a}^{b}x^2 dx$ | 23.4 | 39.2 | 1.2 |

---

```python
# Return the nth item of a fibonacci sequence.
def fib(n):
    if n == 0: return 0
    if n == 1: return 1
    return fib(n-1) + fib(n-2)
```