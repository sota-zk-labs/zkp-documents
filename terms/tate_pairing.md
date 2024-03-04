# Tate Pairing

[Link](https://research.metastate.dev/plonk-by-hand-part-1/)

Consider the following functions, defined via their [divisors](divisor.md):

- $F_P = n [P] - n [O]$, where $n$ is the order of $G1$, i.e., $n P = O$ for any $P$
- $F_Q = n [Q] - n [O]$
- $g = [P + Q] - [P] - [Q] + [O]$

Now, let’s examine the product $F_P \cdot F_Q \cdot g^n$. The divisor is:
$n [P] - n [O] + n [Q] - n [O] + n [P + Q] - n [P] - n [Q] + n [O]$
which simplifies neatly to:
$n [P + Q] - n [O]$

Notice that this divisor is of exactly the same format as the divisor for $F_P$ and $F_Q$ above. Hence,
$F_P \cdot F_Q\cdot g^n = F_{P + Q}$.

Now, we introduce a procedure called the "final exponentiation" step, where we take the result of our functions above (
$F_P, F_Q$, etc.) and raise it to the power $z = (p^{12} - 1) / n$, where $p^{12} - 1$ is the order of the
multiplicative group in $F_{p^{12}}$ (i.e., for any $x \in F_{p^{12}}, x^{(p^{12} - 1)} = 1$). Notice that if you apply
this exponentiation to any result that has already been raised to the power of $n$, you get an exponentiation to the
power of $p^{12} - 1$, so the result turns into 1. Hence, after final exponentiation, $g^n$ cancels out, and we get
$F_P^z \cdot F_Q^z = F_{P + Q}^z$.

For an implementation of a modified version of the Tate pairing, called the optimal [Ate pairing](ate_pairing.md). The
code implements [Miller's algorithm](miller_algorithm.md), which is needed to actually compute $F_P$.
