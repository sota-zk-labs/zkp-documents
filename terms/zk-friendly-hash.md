---
comments: true
---

# ZK-Friendly Hash

## References

- [ZK-Friendly Hash Blog](https://www.zellic.io/blog/zk-friendly-hash-functions/)
- [New Directions in ZK Hashing](https://www.youtube.com/watch?v=SXnb7T9YATs&ab_channel=ZeroKnowledge)
- [Dealing with Hashes in ZK](https://blog.taceo.io/whats-the-deal-with-hashes-in-zk/)

## Hash Function

A [cryptographic hash function](https://en.wikipedia.org/wiki/Cryptographic_hash_function) is one of the basic primitives for
cryptography. Cryptographic schemes such as digital signatures, message authentication codes, commitment schemes, and authentications
are built on top of hash functions.

## Usage of Hashes in the ZK Protocol

A hash function is also useful in the ZK protocol. One famous example is the membership check in a Merkle tree. For a Merkle root $r$,
the prover will claim knowledge of the witness $w_1, .., w_n$ such that:

$$
\begin{aligned}
H(...H(H(w_ 1, w_ 2), w_ 3))..., w_ n) = r
\end{aligned}
$$

to prove their knowledge of element $w_1$, which is a member of the Merkle tree.

- E.g. [Tornado Cash](https://www.zellic.io/blog/how-does-tornado-cash-work) uses a Merkle tree.

### The Need for ZK-Friendly Hash Function

Most modern ZK-proof systems operate over large prime fields (e.g., 256-bit in [Halo2](https://zcash.github.io/halo2/), 64-bit
in [Plonky2](https://github.com/0xPolygonZero/plonky2), and 31-bit in [Plonky3](https://github.com/Plonky3/Plonky3)).

The efficiency of circuits in zero-knowledge (ZK) protocols largely depends on their algebraic structure. Zero-knowledge-friendly hash
functions are specifically designed to operate directly over large prime fields, minimizing the number of multiplications in the ZK
circuit, which is crucial because the performance cost in ZK-proof systems often relates to these multiplications.

Generally, if the circuit is represented with simple expressions within a large field, it allows for more efficient proofs in terms of
the prover's execution time and the size of the proof.

Unfortunately, traditional hash functions are not suitable for this purpose as they are usually defined to operate on bits, not on
prime field elements. This makes them inappropriate for ZK-proof systems that operate over larger prime fields.

## Exploring ZK-Friendly Hash

We can categorize these hashes into three different classes:

- Low-degree round functions
- Low-degree equivalent round functions
- Lookup-based round functions

### Low-degree Round Functions

The low-degree round function is mapping $y = x^d$ (usually $d$ is either 3, 5, or 7, depending on the prime field).

The advantage is fast in plain, but it requires more rounds to be secure and often needs more constraints.

Some examples of such hashes
are [MiMC](https://eprint.iacr.org/2016/492), [GMiMC](https://eprint.iacr.org/2019/397), [Poseidon](https://eprint.iacr.org/2019/458),
[Poseidon2](https://eprint.iacr.org/2023/323),
and [Neptune](https://eprint.iacr.org/2021/1695).

In total, this approach still allows for greater performance than using standardized hash functions operating on bits like SHA-2, while
remaining relatively straightforward to analyze in terms of cryptanalysis attacks.

### Low-degree Equivalence

This design uses the power map $y = x^{1/d}$. Therefore, it will be slower in plain than the low-degree approach.

On the other hand, it requires fewer rounds for security and has a more efficient representation in proof systems (fewer constraints).

These hash functions are [Rescue](https://eprint.iacr.org/2019/426) (and
Rescue-Prime), [Anemoi](https://eprint.iacr.org/2022/840), [Grendel](https://eprint.iacr.org/2021/984),
and [Griffin](https://eprint.iacr.org/2022/403).

### Lookups

These hashes utilize lookup tables for more cost-effective computations.

The main observation is as follows:

- Decompose field elements into smaller ones over the large prime field.
- Perform a table lookup.
- Compose the result back into a field element.

This approach offers several advantages:

- Fast in plain, cheap in ZK circuits.
- Withstanding algebraic attacks, require a small number of rounds.

The proof system must support lookup arguments to enable these types of hash functions.

There are some hashes, including:

- [Reinforced Concrete](https://eprint.iacr.org/2021/1038):
  - Optimized for large prime fields around 256 bits.
  - Significantly faster performance than other hash functions, but still slower than SHA-3.
  - You can read more about [Reinforced Concrete Hash](terms/reinforced-concrete-hash.md) in our documentation.
- [Tip5](https://eprint.iacr.org/2023/107):
  - Designed for a specialized 64-bit prime field, utilized in systems
      like [Plonky2](https://polygon.technology/blog/introducing-plonky2).
- [Monolith](https://eprint.iacr.org/2023/1025):
  - Expands the design approach to additional fields (the same 64-bit field and a 31-bit field used
      in [Plonky3](https://github.com/Plonky3/Plonky3)).
  - Achieves plain performance comparable to SHA-3 for the first time.

## Designing a New ZK Hash Function

### Design

We have two options to design a new hash:

- Non-invertible compression function (SHA-2 core, Pedersen).
- Sponge based on an invertible transformation (permutation). Keccak, Poseidon, Rescue.

### Requirements

- Native speed: close to mainstream (SHA2/3, BLAKE2/3).
- Security: withstanding third-party cryptanalysis.
- Small circuit: minimizing prover time.

### Battling Algebraic Attacks

To withstand algebraic attacks ([Groebner basis](https://en.wikipedia.org/wiki/Gr%C3%B6bner_basis)), a hash function must be both:

- Of high algebraic degree as a polynomial.
- Irreducible to a small system of low-degree equations.

This seemingly lower bounds the number of rounds in each function. Also, the complexity of algebraic attacks is poorly understood.

### Lookup Arguments as a New Tool

Modern lookup arguments we can use in a hash function:

- [Plookup](https://eprint.iacr.org/2020/315.pdf)
- [Halo2](https://zcash.github.io/halo2/)
- [Caulk](https://eprint.iacr.org/2022/621.pdf)

Allows proving that $x \in T = \{a_1, a_2,..., a_n\}$ for some (not too big) table $T$.
