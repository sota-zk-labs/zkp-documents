---
cards-deck: terms
---

# Embedding Degree []()

Let $E$ be an [elliptic curve](elliptic_curve.md) defined over a finite field $\mathbb{F}_p$, where $n$ is the curve order. The
**embedding degree** of $E$ with respect to $n$ is the smallest integer $k$ such that $n$ divides $p^k - 1$, expressed as
$p^k - 1 = n\times X$.

[](1713278230486)

## Why $p^k - 1 = N \times X$? []()

The embedding process ensures that the group of points of interest can be perfectly replicated within the finite field $\mathbb{F}_p$.

From [this](./elliptic_curve.md#order-of-a-curve): $P \times (n+1) = P$ , so $P \times (p^k - 1 + 1) = P \implies P \times (p^k) = P$.

[](1713280692312)
