---
Title: Seminar Innovative Internet Technologies
Status: Done
Level: 4
Note: Somewhat easy to read
---

# Seminar Innovative Internet Technologies

## Introduction

[Zero Knowledge Proofs (ZKP)](../../terms/zkp.md)

## What are Zero Knowledge Proofs?

[Zero Knowledge Proofs (ZKP)](../../terms/zkp.md)

### Framework

[Zero Knowledge Proofs (ZKP)](../../terms/zkp.md)

### Properties of a ZKP

[Zero Knowledge Proofs (ZKP)](../../terms/zkp.md)

### Non-Interactive ZKP

[Zero Knowledge Proofs (ZKP)](../../terms/zkp.md)

### Proof of Knowledge

[Zero Knowledge Proofs (ZKP)](../../terms/zkp.md)

### Example: Blackbox Workflow of a ZKP

[Zero Knowledge Proofs (ZKP)](../../terms/zkp.md)

## Examples of Modern ZKPs

[Zero Knowledge Proofs (ZKP)](../../terms/zkp.md)

### zk-SNARKs

[zkSNARK](../../terms/zkSNARK.md)

### zk-STARKs

[zkSTARK](../../terms/zkSTARK.md)

### Bulletproof [more](https://medium.com/coinmonks/zero-knowledge-proofs-using-bulletproofs-4a8e2579fc82)

Can prove that a committed secret value $v \in Z_p$ is in a given range \[0, 2n − 1\]

- No trusted setup (using [fiat_shamir](../../terms/fiat_shamir.md)).
- Can batch multiple proofs into "one" proof.

### Ligero

### Sonic

### Comparison

| Name        | Trusted Setup | Proof Size          | Proving Time              | Verification Time  |
|-------------|---------------|---------------------|---------------------------|--------------------|
| Bulletproof | No            | O(log M)            | O(M)                      | O(M)               |
| Ligero      | No            | O($\sqrt{\|C\|}$)   | $\|C\| \log \|C\|$        | $\|C\| \log \|C\|$ |
| STARK       | No            | O($(\log \|C\|)^2$) | O($(\|C\| \log \|C\|)^2$) | O($\|C\|$)         |
| Sonic       | Yes           | O(1)                | O($\|C\| \log \|C\|$)     | $N + \log \|C\|$   |

$\|C\|$ is the number of gates of the computation expressed as an arithmetic circuit, $M$ the number of *And* gates in
it, $N$ the length of the inputs and outputs of the computation.

## Use Cases

### Signatures

### Private Transactions on Blockchain

### Verifying Computations

## Related Works

## Conclusion
