---
cards-deck: terms
---

# Diophantine Set

## Definition []()

Read the definition of [Diophantine equation](diophantine_equation.md) first.

> [!NOTE]
> A set $S \in \mathbb{Z}^k$ is called Diophantine if and only if there exists an integer-coefficient multivariate polynomial $R_S$
> such that $\mu \in S \Leftrightarrow \exists \omega \in \mathbb{Z}^{k'}$ such that $R_S(\mu, \omega)=0$, i.e., $\mu \in S$ if $\mu$
> is a part of a solution for a fixed Diophantine equation. We call $R_S$ a **representing polynomial** of $S$, and $\omega$ an
> auxiliary witness.

Consider the Diophantine equation: $$\mu = \omega_1 \cdot \omega_2$$

- Here, $\mu$ is a parameter, and $\omega_1$ and $\omega_2$ are unknowns.
- The equation has a solution in $\omega_1$ and $\omega_2$ precisely when $\mu$ can be expressed as a product of two integers greater
  than 1 (i.e., when $\mu$ is a composite number).

[](1713611052650)

## MRDP Theorem []()

The MRDP theorem states that any recursively enumerable set can be represented by a Diophantine equation.

[Diophantine Sets] = [Computably Enumerable Sets]

[](1713611052653)

### Computably Enumerable Sets

A set $S$ is computably enumerable if and only if there is an algorithm that halts if the input is a member of $S$, and runs forever
if otherwise.

Or, a set $S$ is computably enumerable if there is an algorithm (not necessarily halting) that enumerates the members of $S$.

## Fact

Suppose we have two Diophantine sets $S_1$ and $S_2$, respectively representing polynomials $P_1,P_2$. Then:

- $R_{S_1 \cup S_2}(\mu; \omega_1, \omega_2)=P_1(\mu_1, \omega_1) \cdot P_2(\mu_2, \omega_2)$
- $R_{S_1 \cap S_2}(\mu; \omega_1, \omega_2)=P_1(\mu_1, \omega_1)^2 + P_2(\mu_2, \omega_2)^2$
