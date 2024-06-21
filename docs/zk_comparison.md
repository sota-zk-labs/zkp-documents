---
comments: true
---

# Zk Comparison

## Summary

| Name                   | Tech                     | Note                                               |
|------------------------|--------------------------|----------------------------------------------------|
| ZkSync                 | [PLONK](plonk.md) + FRI  |                                                    |
| dYdX (StarkEx)         | PLONK + FRI              |                                                    |
| Polygon Zero (Plonky2) | PLONK + FRI              |                                                    |
| Polygon Hermez         | [PLONK + FRI] + Groth16  |                                                    |
| Zcash (Halo2)          | PLONK + IPA/Bulletproofs | Shortest proofs among transparent SNARKs. Slow $V$ |
| Scroll                 | PLONK + KZG              | Modified from Halo2                                |
| Linea                  | PLONK + Groth16          |                                                    |
| Loopring               | Groth16                  |                                                    |

## Brief Comparison

### STARK

STARK = PLONK + FRI

STARKs, Fractal, Aurora, Virgo, Ligero++

Pros: Shortest proofs amongst plausibly post-quantum SNARKs.  
Cons: Proofs are large (100s of KBs depending on security).

### MIPs and IPs + [fast-prover Polynomial commitments]

Examples: Spartan, Brakedown, Orion, Orion+(HyperPlonk).

Pros: Fastest $P$ in the literature, plausibly post-quantum + transparent if polynomial commitment is.  
Cons: Bigger proofs than 1. and 2. above.

### Linear-PCP Based

Example: Groth16

Pros: Shortest proofs (3 group elements), fastest $V$.  
Cons: Circuit-specific trusted setup, slow and space-intensive $P$, not post-quantum.

### Constant-round polynomial IOP + KZG polynomial commitment

Examples: Marlin-KZG, PlonK-KZG

Pros: Universal trusted setup.  
Cons: Proofs are ~4x-6x larger than Groth16, $P$ is slower than Groth16, also not post-quantum.  
Counterpoint for $P$: Can use more flexible intermediate representations than circuits and R1CS.

---

See [chapter_19](../articles/proofs-arguments-and-zero-knowledge/chapter_19.md) for further details.
