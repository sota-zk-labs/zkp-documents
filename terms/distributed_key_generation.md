---
comments: true
---
# Distributed Key Generation

Distributed Key Generation (DKG) allows $n$ participants to collectively generate a pair of public and secret keys. While the public
key is visible by everyone, the private key is separated into $n$ parts, with each participant receiving one part.

A $(t, n)$ DKG protocol has the following properties:

- Any $t+1$ honest parties can reconstruct the same $sk$
- All honest parties agree on the same value of $pk = E(sk)$
- $sk$ is uniformly distributed in $\mathbb{Z}_p$

## References

- [Orochi Network's cookbook](https://docs.orochi.network/dkg/verifiable-secret-sharing/chapter.html)
