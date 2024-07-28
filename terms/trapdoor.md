---
comments: true
---

# Trapdoor

> [!NOTE]
> A trapdoor is a secret piece of information that enables efficient decryption or other cryptographic operations which
> would be infeasible without it.

Trapdoors are fundamental to the construction of many cryptographic systems, including public-key
encryption schemes, digital signatures, and certain lattice-based cryptographic protocols.

## Characteristics of a Trapdoor

1. **Secret Knowledge**: The trapdoor is a secret key or piece of information known only to authorized parties.
2. **Asymmetry**: Cryptographic operations with the trapdoor (e.g., decryption, signing) are efficient, while without the trapdoor,
   these operations are computationally infeasible.
3. **One-Way Function**: Often associated with one-way functions or trapdoor functions, where computing the function is easy, but
   inverting it without the trapdoor is hard.

## Applications of Trapdoors

1. **Public-Key Cryptography**:
    - **RSA**: The prime factors of the modulus $n = pq$ act as the trapdoor. Knowing the prime factors allows efficient decryption
      and signature creation.
    - **ElGamal**: The discrete logarithm acts as the trapdoor. Knowing the discrete log of the public key enables decryption and
      signing.

2. **Digital Signatures**:
    - **DSA**: The private key is the trapdoor that enables signing a message. Verifying the signature, however, does not require the
      trapdoor.
    - **ECDSA**: The private key in elliptic curve cryptography allows for efficient signing.

3. **Lattice-Based Cryptography**:
    - **Learning With Errors (LWE)**: A matrix with a trapdoor allows efficient sampling from certain distributions over lattices,
      enabling decryption and other operations.
    - **NTRU**: The private key is used as a trapdoor to efficiently decrypt messages encrypted with the public key.

## Example

### Trapdoor in RSA

1. **Key Generation**:
    - Select two large prime numbers $p$ and $q$.
    - Compute the modulus $n = pq$.
    - Compute the totient $\phi(n) = (p-1)(q-1)$.
    - Choose a public exponent $e$ such that $1 < e < \phi(n)$ and $\gcd(e, \phi(n)) = 1$.
    - Compute the private exponent $d$ such that $ed \equiv 1 \pmod{\phi(n)}$.
2. **Public Key**: $(n, e)$
3. **Private Key (Trapdoor)**: $(p, q)$ or $d$
4. **Encryption**:
    - Given a message $m$, the ciphertext $c$ is computed as $c \equiv m^e \pmod{n}$.
5. **Decryption**:
    - Using the private key (trapdoor) $d$, the plaintext $m$ is recovered as $m \equiv c^d \pmod{n}$.

Without the trapdoor (knowledge of $d$ or the prime factors $p$ and $q$), decryption would require solving the hard problem of
integer factorization, which is computationally infeasible for sufficiently large $n$.

### Trapdoor in Lattice-Based Cryptography

In lattice-based cryptography, trapdoors are used to solve instances of hard lattice problems efficiently. A notable example is the use
of trapdoors in LWE-based encryption schemes.

1. **Key Generation**:
    - Generate a random matrix $\mathbf{A} \in \mathbb{Z}_q^{m \times n}$.
    - Construct a trapdoor $\mathbf{T}$ for $\mathbf{A}$.
2. **Public Key**: Matrix $\mathbf{A}$
3. **Private Key (Trapdoor)**: $\mathbf{T}$
4. **Encryption**:
    - Encode the message $m$ as a vector and compute the ciphertext $\mathbf{c}$ using $\mathbf{A}$.
5. **Decryption**:
    - Using the trapdoor $\mathbf{T}$, solve the system of equations to recover $m$.

The trapdoor $\mathbf{T}$ allows for efficient decryption by providing a way to solve the underlying hard problem (e.g., bounded
distance decoding) that would be infeasible otherwise.
