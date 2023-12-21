# Pairings or Bilinear Maps

Read the full article on pairings or bilinear
maps [here](https://alinush.github.io/2022/12/31/pairings-or-bilinear-maps.html).

## Definition

A function $e$ is considered a bilinear function or map if it satisfies the following conditions:

- Let $\mathbb{G}_1$, $\mathbb{G}_2$, and $\mathbb{G}_T$ be cyclic groups of order $n$. The bilinear pairing is
  represented as $e : \mathbb{G}_1 \times \mathbb{G}_2 \rightarrow \mathbb{G}_T$.

    - **Bilinearity**: $e(aP, bQ) = e(P, Q)^{ab}$.

    - **Non-degeneracy**: $e(P, Q) \neq 1$.

    - **Computability**: $e(P, Q)$ can be computed efficiently.

## Properties

- $e(aP, bQ) = e(P, Q)^{ab}$

- $e(P, {a}Q) = e(P, Q)^{a}$

- $e(P, Q + R) = e(P, Q) \cdot e(P, R)$

## Example

Consider simple numbers $P$, $Q$, $R$, and $S$. Creating a pairing can be done using $e(x, y) = 2^{x \cdot y}$. Then,
observe:

> $e(6, 4) \cdot e(6, 5) = 2^{{6} \cdot {4}} \cdot 2^{{6} \cdot {5}} = 2^{{6} \cdot ( {4} + {5})} = 2^{{6} \cdot {9}}$
>
> $e(6, 4 + 5) = 2^{{6} \cdot {9}}$

> $e(6 \cdot 2, 4 \cdot 3) = 2^{{6} \cdot {2} \cdot {4} \cdot {3}}$
>
> $e(6, 4)^{{2} \cdot {3}} = 2^{{6} \cdot {4} \cdot {2} \cdot {3}}$

## What Can It Do?

The expression $e(P, Q) \cdot e(G, G \cdot 5) = 1$ is equivalent to $p \cdot q + 5 = 0$.