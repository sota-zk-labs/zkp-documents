---
comments: true
cards-deck: terms
---

# Trapdoor For Uniform Random Matrix

## Definition []()

The [trapdoor](trapdoor.md) $R$ is a **short** matrix such that given a uniform random matrix $A$, we have:

$$A \cdot R = G$$

where $G$ is a [gadget matrix](gadget_matrix.md).

[](1724491879755)

## Preimage Sampling for Short Integer Solution (SIS)

- Let $f_A(x) := Ax$
- Given $u = f_A(x)$ and $R$, we can sample short $x'$ where $f_A(x') = u$

> [!NOTE]
> The trapdoor allows us to find such a vector $x'$. Without it, finding $x'$ is hard.

## Properties

Suppose $A = [A_1 | A_2]$. There are two statistically indistinguishable ways to sample $f_A^{-1}(u)$:

- **Formula 1**: If $R_1$ is a trapdoor for $A_1$, then $A_1 R_1 = G$, and:

$$
[A_1 | A_2] \cdot
\begin{bmatrix}
R_1 \\
0
\end{bmatrix}
= G
$$

- **Formula 2**: If $A_2 = A_1 R_2 \pm G$ for short $R_2$, then:

$$
[A_1 | A_2] \cdot
\begin{bmatrix}
\mp R_2 \\
I
\end{bmatrix}
= G
$$
