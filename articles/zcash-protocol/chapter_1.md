---
Title: Introduction
Status: Done
Level: "1"
---

# Chapter 1: Introduction

---
Zcash, an evolution of the Zerocash protocol, bridges the gap between transparent Bitcoin transactions and shielded payments enabled
by [zk-SNARKs](../../terms/zkSNARK.md).

**Concepts and Abstractions:**

- **Zero-knowledge proofs:**The magic behind Zcash's shielded transactions. These cryptographic tools allow users to prove the validity
  of transactions without revealing their details, enabling private spending.
- **Shielded addresses:**These special addresses mask spending and receiving addresses, further enhancing privacy.
- **Sapling:**The upgraded protocol was introduced in 2018, offering smaller and faster transactions compared to its predecessor,
  Sprout.

**Protocol Deep Dive:**

- **Abstract protocol:**Defines the ideal components of Zcash, including functions for generating proofs, verifying their validity, and
  managing shielded addresses.
- **Concrete protocol:**Explains how these ideal functions are implemented using specific cryptographic algorithms and data structures.
- **Network upgrades:**Outlines the process for introducing new features and functionality to Zcash over time, ensuring its ongoing
  development and evolution.

**Beyond Transparency:**

- **Consensus changes from Bitcoin:**Zcash deviates from Bitcoin's Proof-of-Work consensus mechanism to accommodate shielded
  transactions efficiently.
- **Differences from Zerocash:**The document analyzes the key modifications Zcash made to the original Zerocash protocol, improving
  security, performance, and usability.

**Technical Appendix:**

- **Circuit design:**Provides detailed insights into how Sapling circuits, the mathematical core
  of [zk-SNARKs](../../terms/zkSNARK.md), are designed and implemented.
- **Batching optimizations:**Explains techniques for verifying multiple signatures and proofs simultaneously, improving efficiency and
  scalability.

## 1.1 High-level Overview

---
> [!WARNING]
> This is the high-level idea, so it is imprecise in some aspect.

- There are two type of transactions in Zcash:
  - Transparent transaction (similar to Bitcoin's).
  - Shielded (encrypt) transaction (3 kinds: Sprout, Sapling, Orchard).
- Shielded transactions contain amounts, shielded addresses, spending keys, and commitments for verification. To prevent
  double-spending, nullifies linked to spending keys to invalidate used transactions.
- Transactions can combine transparent and shielded parts, with special descriptions for shielded
  transfers. [zk-SNARKs](../../terms/zkSNARK.md) ensure transaction validity and privacy without revealing any details.
- Shielded addresses include transmission keys for secure note communication between parties.
- Sapling and Orchard allow for full viewing keys, granting authorized users the ability to see a note's content without the power to
  spend it.
- Spending proves a note existed but not its origin, making linking notes difficult. This contrasts with mixing-based privacy methods
  with smaller traceable sets.
