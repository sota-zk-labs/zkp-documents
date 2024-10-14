---
cards-deck: terms
---
# Learning With Errors

Learning With Errors (LWE) is a foundational problem in lattice-based cryptography and forms the basis for many cryptographic schemes
due to its hardness. The problem can be described as follows:

**References:**

+ [Learning with errors: Encrypting with unsolvable equations (highly recommended)](https://www.youtube.com/watch?v=K026C5YaB3A)
+ [The Learning with Errors Problem](https://people.csail.mit.edu/vinodv/CS294/lecture1.pdf)

## The LWE Problem []()

LWE involves solving a system of noisy linear equations. More formally, the LWE problem can be defined as follows:

1. **Secret Vector**: There is a secret vector $\mathbf{s} \in \mathbb{Z}_q^n$, where $\mathbb{Z}_q$ denotes the integers modulo
   $q$.

2. **Public Information**: There is a matrix $\mathbf{A} \in \mathbb{Z}_q^{m \times n}$ and a noise vector $\mathbf{e} \in\mathbb{Z}_q^m$. The entries of $\mathbf{A}$ are chosen uniformly at random from $\mathbb{Z}_q$, and the entries of
   $\mathbf{e}$ are typically chosen from some error distribution (often a discrete Gaussian distribution or a uniform distribution
   over a small range).

> [!NOTE]
>
> The LWE problem provides a set of pairs $(\mathbf{A}, \mathbf{b})$, where
> $\mathbf{b} = \mathbf{A} \cdot \mathbf{s} + \mathbf{e} \pmod q$. The goal is to recover the secret vector $\mathbf{s}$ given
> $\mathbf{A}$ and $\mathbf{b}$.

[](1724465459039)

## Computational vs. Decisional LWE

+ **Computational LWE**: Given $(\mathbf{A}, \mathbf{b})$, find the secret vector $\mathbf{s}$.
+ **Decisional LWE**: Distinguish between pairs $(\mathbf{A}, \mathbf{b})$ where
  $\mathbf{b} = \mathbf{A} \cdot \mathbf{s} + \mathbf{e}$ and pairs $(\mathbf{A}, \mathbf{b})$ where $\mathbf{b}$ is uniformly random.

## Applications of LWE in Cryptography

LWE's hardness is used to construct various cryptographic primitives:

1. **Public-Key Encryption**: LWE can be used to design secure public-key encryption schemes. An example is the Regev encryption
   scheme, which is based on the LWE problem.
2. **Homomorphic Encryption**: LWE allows for the construction of fully homomorphic encryption schemes, enabling computations on
   encrypted data.
3. **Digital Signatures**: LWE-based digital signature schemes provide secure and efficient signature generation and verification.
4. **Key Exchange Protocols**: LWE can be used to design secure key exchange protocols resistant to quantum attacks.
5. **Identity-Based Encryption**: LWE supports the construction of identity-based encryption schemes, where the public key can be
   derived from a user's identity (e.g., email address).

## Hardness and Security

The security of LWE-based schemes relies on the assumed hardness of the LWE problem. This hardness can be reduced to worst-case
hardness assumptions about [lattice](lattice.md) problems:

1. **Worst-Case to Average-Case Reduction**: Solving LWE in the average case is as hard as solving certain lattice problems (like the
   Shortest Vector Problem) in the worst case.
2. **Quantum and Classical Hardness**: LWE is believed to be hard both classically and quantumly, making it a strong candidate for
   post-quantum cryptography.

## Parameters and Trade-offs

+ **Modulus $q$**: Typically a large prime number. The choice of $q$ affects the security and efficiency of the scheme.
+ **Dimension $n$**: The dimension of the secret vector. Larger $n$ increases security but also computational complexity.
+ **Number of Samples $m$**: The number of LWE samples. There is a trade-off between the number of samples and the hardness of the
  problem.
