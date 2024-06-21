---
comments: true
---

# Zero knowledge Succinct Non-interactive Arguments of Knowledge (zkSNARK)

## Definition

[zkp.md](zkp.md)

[succinct.md](succinct.md)

[interactive.md](interactive.md)

[arguments.md](arguments.md)

## Types

IPs, MIPs, and PCPs/IOPs can all be transformed into succinct interactive arguments by combining them with a
cryptographic primitive called a [polynomial commitment scheme](polynomial-commitment/000_polynomial_commitment.md).

Transformations from linear PCPs to arguments are somewhat different, though closely related to certain polynomial
commitment schemes.

The interactive arguments can then be rendered non-interactive and publicly verifiable by applying a cryptographic
technique called the FiatShamir transformation

### Interactive proofs (IPs)

### Multi-prover interactive proofs (MIPs)

### Probabilistically checkable proofs (PCPs)

### Interactive oracle proofs (IOPs)

### Linear PCPs
