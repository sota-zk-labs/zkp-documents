# Prime Or Finite Fields

## Definition

A prime field $\mathbb{F}_p$ consists of the set of numbers $0, 1, 2, \ldots, p-1$, where $p$ is prime, and the various
operations are
defined as follows:

- $a + b:  (a + b) \pmod p$
- $a * b:  (a * b) \pmod p$
- $a - b:  (a - b) \pmod p$
- $a / b:  (a * b^{p-2}) \pmod p$

In essence, all mathematical operations are performed modulo $p$.

### Order of The Multiplicative Group

Given a positive integer $n$ and an integer
$a$ [coprime](https://en.wikipedia.org/wiki/Coprime "Coprime") to $n$, the **multiplicative order** of $a$ modulo $n$ is
the
smallest positive integer $k$ such that $a^k ≡ 1 \pmod n$

According to the [Fermat's little theorem](fermat_little_theorem.md) $k = n-1$ with $n$ is a prime number.

## Why Choose Prime Fields

### Prime Fields Vs Real Numbers

The [Fundamental Theorem of Algebra](https://en.wikipedia.org/wiki/Fundamental_theorem_of_algebra) guarantees that
complex numbers, being a [quadratic extension](quadratic_field.md) of real numbers, are "complete" and cannot be further
extended with new elements satisfying algebraic relationships. However, ==with prime fields, such limitations do not
exist==, allowing for cubic extensions and higher-order
extensions. [Elliptic curve pairings](elliptic_curve_pairings.md) are constructed using these supercharged modular
complex numbers derived from such extensions.

In simpler terms:

> [!NOTE]  
> While we cannot find the root of $f(x) = \sqrt{-1}$ using real numbers, we can achieve this using complex numbers or
> prime fields.
