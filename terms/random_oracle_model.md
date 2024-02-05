# Random Oracle Model (ROM)

## Random Oracle Model

The ==random oracle model== (**ROM**) is an idealized setting designed to capture the fact that cryptographers have developed hash
functions (e.g., [SHA-3](https://en.wikipedia.org/wiki/SHA-3) or [BLAKE3](https://en.wikipedia.org/wiki/BLAKE_(hash_function)#BLAKE3))
that efficient algorithms seem totally unable to distinguish from random functions. It means
that in the ROM, one cannot differentiate between hash functions and random functions.

By a random function
$R$:  $\mathbb{D} \rightarrow \lbrace 0, 1\rbrace^k$, on any input $x \in \mathbb{D}$, $R$ chooses its output $R(x)$ uniformly at
random from $\lbrace 0, 1 \rbrace^k$.

## Random Oracle

Accordingly, the **ROM** simply assumes that the prover and verifier have query access to a random function $R$. This means that there
is an oracle (called a ==random oracle==) where the prover and verifier can submit any query $x$, and the oracle will return $R(x)$.
This random oracle also keeps a record of its responses to make sure that it repeats the same response if $x$ is queried again.

In the real world, random oracle is not valid because listing the value $R(x)$ for every input $x \in \mathbb{D}$ is not feasible,
especially
when dealing with a huge $\mathbb{D}$ (e.g., $|D| \ge 2^{256}$).  So, it is often replaced with a concrete hash function like
**SHA-3**, which is
succinctly specified via, e.g., a small circuit or computer program that evaluates the hash function on any input.

Although, in principle, a cheating prover can use this succinct representation (small circuit, computer program,..) to break the
security of the protocol, the protocols proven to be secure in the **ROM** are often considered secure in practice. Indeed, no
deployed protocols have been broken in this manner.
