---
comments: true
cards-deck: terms
---
# Schnorr Signature []()

The **Schnorr signature** is a digital signature scheme that provides a way to verify the authenticity of a message or 
document. The Schnorr signature involves two phases: generation and verification.

Let $G$ be a group of prime order $q$ with $g$ as a generator of $G$. Let $H$ be a hash function, and let the number $s$ in the group
$G$ be $g^s$.

**Generation**:

- Sample a random nonce $k \in \mathbb{Z}_q$ and compute the commitment: $R = g^k \in G$
- Compute the challenge $c = H(R, Y, m)$  (where $Y$ is the group public key, $m$ is the message and $H$ is the hash function)
- Using the secret key $s$, compute the response $z = k + s \cdot c \in \mathbb{Z}_q$
- Define the signature over $m$ as $\sigma = (R, z)$

**Verification**:

- Parse $\sigma = (R, z)$ and derive $c = H(R, Y, m)$
- Compute $R' = g^z \cdot Y^{-c}$
- Verify that: $R' \stackrel{?}{=} R$

[](1724491474259)

## References

[FROST paper](https://eprint.iacr.org/2020/852.pdf).
