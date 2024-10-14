---
comments: true
cards-deck: terms
---

# Correlation-Intractability (CI) []()

A hash function family $H$ is called correlation-intractable if given a random function from $H$, for all sparse relations, it is hard
to find an input-output pair that satisfies the relation.

## Details

Let denote a relation $R(a, b)$. A hash family $H$ satisfies **CI** for $R$ if it is computationally infeasible (given a hash function
$h \leftarrow H$) to
find a pair $(y, h(y))$ such that $R(y, h(y))$ is true.

[](1724427554813)
## Example

Suppose $I$ is an [IP](ip.md) for a [language](language.md) $L$ such that $I$ satisfies
[round-by-round soundness](../articles/proofs-arguments-and-zero-knowledge/chapter_5.md#Round-by-round%20Soundness%20Requirements) .\
Let $R$ denote the relation capturing “success” of a cheating prover for the [Fiat-Shamir](fiat_shamir.md) transformation $Q$ of $I$.\
So, we define $R(a, b) = true$ if $(a, b) = (y, h(y))$ such that $y = h(x, g_1,...,g_i)$ with $x \notin L$. For any $h(y)$ in $R$,
$I$ is in a doomed state at the start of round $i$, but enters a non-doomed state if verifier sends $h(y)$ at this round.

A cheating prover in the [Fiat-Shamir](fiat_shamir.md) protocol $Q$ must find some pair $(y,h(y))$ satisfying property $R$ to find a
convincing “proof” of membership in $L$ for some $x \notin L$.
If $H$ satisfies **CI** for $R$, then no polynomial time cheating prover can find a convincing proof of a false statement with
non-negligible probability.
