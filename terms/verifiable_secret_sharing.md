---
comments: true
cards-deck: terms
---
# Verifiable Secret Sharing

## Distributed Key Generation

Read the definition of DKG [here](./distributed_key_generation.md).

## Verifiable Secret Sharing (VSS)

### Definition []()

A $(k, n)$ VSS includes two phases: *Sharing* and *Reconstruction* as follows:

**Share:**

- Dealer $D$ has a secret $s$. There are $n$ parties $P_1,\dots,P_n$.
- After several rounds of interaction among the parties, each party holds a share $s_i$.

**Reconstruct**:

- Each party $P_i$ publishes its share $s_i$ from the sharing phase for reconstructing $s$.

If $D$ is dishonest, then at the end of **sharing** phase, there exists a value $s^*$ such that all parties agree on it at the end of
**reconstruct** phase.

[](1724492402758)

## Pedersen Construction 

We describe a VSS protocol from **Pedersen**.

### The Commitment Scheme

Let $p, q$ be large primes such that $q$ divides $p-1$ and let $G_q$ be the unique subgroup of $\mathbb{Z}^*_p$ of order $q$. Let $g$
and $h$ be elements of $G_q$ where $g$ is the generator of $G_q$ and no one knows the value $d$ such that $h = g^d$. These elements
can be chosen using a coin-flipping protocol.

The committer commits to its secret $s \in \mathbb{Z}_q$ by choosing a random $t \in \mathbb{Z}_q$, then computing and broadcasting
$E(s, t) = g^sh^t$. Such a commitment can later be opened by revealing $s$ and $t$.

If the committer knows $d = log_g(h)$, he can commit to a value $s$ and then can falsely claim that he committed to $s'$ because:
$$g^sh^t = g^{s'}h^{t'} \iff g^{s - s'} = h^{t'-t} \iff log_gh = \dfrac{s- s'}{t'-t}$$

### Verification of Shares

Assume that a dealer $D$ has a secret $s$ and wants to create a $(k,n)$ VSS protocol with $n$ parties $P_1,\dots, P_n$.

Here is the scheme:

- $D$ publishes a commitment to $s$: $E_0 = E(s, t)$ where $E(s, t) = g^sh^t$. for a random $t$
- $D$ chooses $F \in \mathbb{Z} _ q[x]$ of degree at most $k-1$: $F(x) = s + F _ 1x + \dots + F _ {k-1}x ^ {k-1}$
- $D$ computes $s_i = F(i)$ for $i = 1,\dots,n$
- $D$ chooses $G_1,\dots, G_{k-1}$ at random and broadcasts the commitments $E_i = E(F_i, G_i)$
- Let $G(x) = t + G_1x + \dots G_{k-1}x^{k-1}$
- $D$ computes $t_i = G(i)$ for $i = 1, \dots, n$

**Share**:

- $D$ sends a tuple $(s_i, t_i)$ to $P_i$ for $i = 1, \dots, n$
- Each $P_i$ verifies their share $(s_i, t_i)$ by checking: $E(s_i, t_i) \stackrel{?}{=} \prod_{j=0}^{k-1}E_j^{i^j}$

**Reconstruct**:

- Let $S \subset \lbrace 1,\dots,n \rbrace$ be a subset of size $k$. The participants in $S$ find two unique polynomials: $F'$ and
  $G'$ of degree at most $k-1$ satisfying:

  - $F'(i) = s_i$
  - $G'(i) = t_i$
- It is sufficient to put $s' = F'(0)$ and $t' = G'(0)$ such that $E_0 = E(s', t')$.
- $S$ can compute $s' = \sum_{i \in S}s_i a_i$  and can also find $t' = \sum_{i \in S}t_i a_i$ where
  $a_i = \prod_{j \in S, j \ne i}\dfrac{i}{i-j}$

## FROST

Read the section of FROST [here](./frost.md).

## References

[Orochi Network's cookbook](https://docs.orochi.network/dkg/verifiable-secret-sharing/pedersen-construction.html)

[Non-Interactive and Information-Theoretic Secure Verifiable Secret Sharing](https://link.springer.com/chapter/10.1007/3-540-46766-1_9)
