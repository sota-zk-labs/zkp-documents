---
comments: true
---

# Cyclotomic Polynomials and Primitive Roots of Unity

## Introduction

<https://www.youtube.com/watch?app=desktop&v=M5WMx498wLQ>

Cyclotomic polynomials and primitive roots of unity are fundamental concepts in algebra and number theory. They play crucial roles in
fields such as cryptography, coding theory, and signal processing. This document provides an overview of these concepts, their
properties, and their applications.

## Cyclotomic Polynomials

### Definition

The $n$-th cyclotomic polynomial, denoted $\Phi_n(x)$, is defined as the polynomial whose roots are the primitive $n$-th roots of
unity. Specifically,

$$\Phi_n(x) = \prod_{\substack{1 \leq k \leq n \\ \gcd(k, n) = 1}} \left( x - e^{2\pi i k/n} \right)$$

where $e^{2\pi i k/n}$ are the $n$-th roots of unity, and $\gcd(k, n) = 1$ ensures that we only take the primitive roots.

### Properties

1. **Degree**: The degree of $\Phi_n(x)$ is $\varphi(n)$, where $\varphi$
   is [Euler's totient function](https://www.geeksforgeeks.org/eulers-totient-function/).
2. **Integer Coefficients**: $\Phi_n(x)$ has integer coefficients.
3. **Irreducibility**: $\Phi_n(x)$ is irreducible over the field of rational numbers $\mathbb{Q}$.
4. **Recurrence Relation**: Cyclotomic polynomials satisfy the relation:

$$x^n - 1 = \prod_{d|n} \Phi_d(x)$$

This implies that cyclotomic polynomials can be derived from the polynomial $x^n - 1$ by factoring out polynomials corresponding to
divisors of $n$.

### Examples

- $\Phi_1(x) = x - 1$
- $\Phi_2(x) = x + 1$
- $\Phi_3(x) = x^2 + x + 1$
- $\Phi_4(x) = x^2 + 1$
- $\Phi_5(x) = x^4 + x^3 + x^2 + x + 1$
- $\Phi_6(x) = x^2 - x + 1$
- $\Phi_{12}(x) = x^4 - x^2 + 1$

### Example Calculation

For $n = 6$:

$$x^6 - 1 = (x^3 - 1)(x^3 + 1) = (x-1)(x^2 + x + 1)(x+1)(x^2 - x + 1)$$

Therefore, the cyclotomic polynomials are:

- $\Phi_1(x) = x - 1$
- $\Phi_2(x) = x + 1$
- $\Phi_3(x) = x^2 + x + 1$
- $\Phi_6(x) = x^2 - x + 1$

## Primitive Roots of Unity

### Definition

A primitive $n$-th root of unity is a complex number $\zeta$ such that $\zeta^n = 1$ and $\zeta^k \neq 1$ for $1 \leq k < n$. In other
words, $\zeta$ is a root of the polynomial $x^n - 1$ but not of any $x^k - 1$ for $k < n$.

### Properties

1. **Existence**: For every positive integer $n$, there are exactly $\varphi(n)$ primitive $n$-th roots of unity.
2. **Multiplicative Group**: The set of all $n$-th roots of unity forms a cyclic group under multiplication.
3. **Cyclotomic Field**: The field extension $\mathbb{Q}(\zeta_n)$, where $\zeta_n$ is a primitive $n$-th root of unity, is called the
   $n$-th cyclotomic field. It has degree $\varphi(n)$ over $\mathbb{Q}$.

### Example

Consider $n = 3$. The primitive 3rd roots of unity are the solutions to $x^3 - 1 = 0$ that are not solutions to $x - 1 = 0$. These are:

$$\zeta_3 = e^{2\pi i / 3} \quad \text{and} \quad \zeta_3^2 = e^{4\pi i / 3}$$

These roots can be expressed in terms of trigonometric functions:

$$\zeta_3 = -\frac{1}{2} + i \frac{\sqrt{3}}{2} \quad \text{and} \quad \zeta_3^2 = -\frac{1}{2} - i \frac{\sqrt{3}}{2}$$

## Applications

### Cryptography

Cyclotomic fields and polynomials are used in constructing certain types of cryptographic systems, including some lattice-based
cryptosystems and fully homomorphic encryption schemes. The structure and properties of cyclotomic fields provide a rich algebraic
framework that is useful for these applications.

### Coding Theory

In coding theory, cyclotomic cosets and polynomials play a role in the construction of BCH codes and other error-correcting codes.
These codes are essential for reliable data transmission over noisy channels.

### Signal Processing

Primitive roots of unity are used in the Discrete Fourier Transform (DFT), which is a fundamental tool in signal processing. The DFT
decomposes a sequence of values into components of different frequencies, leveraging the properties of roots of unity.
