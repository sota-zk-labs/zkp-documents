# Divisor

[Link to Source](https://crypto.stackexchange.com/questions/55342/i-cannot-understand-the-concept-of-a-divisor-for-an-elliptic-curve)

## Definition

Divisors offer a method to track the locations where a function becomes zero or infinite.

$D = n_1P_1 + n_2P_2 + \ldots + n_kP_k$

Here, $P_i$ represents [projective points](homogeneous_polynomial_or_projective_model.md) on the curve (some $P_i$ might
be points at infinity), and $n_i$ are integers.

## How to Understand This?

Consider a function like $f(x) = x^2 - x + 6$. It has two zeroes: $-2$ and $3$. If you were given only these two zeroes,
you could recreate the original function, with the exception of a constant factor.

In pairing-based cryptography, divisors are employed because the pairing function itself is defined as a function with a
specific divisor. Knowing the divisor (and thus the zeroes) is sufficient to reconstruct the function.

> [!NOTE]  
> A divisor is simply an alternative representation of a function.

## Divisor of Rational Functions

Divisors corresponding to [rational functions](rational_function.md) of curves ==always have a degree of $0$== (a consequence of Bezout's theorem).

## Example

Given: $P = (P_x, P_y)$

And: $f(x, y) = x - P_x$

We have: $D = [P] + [-P] - 2 \cdot [O]$

Explanation:

- The function becomes zero at $P$ because $x$ is equal to $P_x$, making $x - P_x = 0$.
- The function becomes zero at $-P$ since $-P$ and $P$ share the same $x$-coordinate.
- To ensure the degree is $0$ with ($n_1 = n_2 = 1$): $n_3 = -2$.