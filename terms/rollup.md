---
comments: true
---

# Rollups: Streamlining Blockchain Scalability

Rollups are designed to enhance blockchain scalability by simplifying transaction processing. The key concept involves
managing multiple transactions off-chain, consolidating them into a single batch, and then submitting this batch as a
unified action to the main blockchain.

The result is a notable reduction in transaction processing times and gas fees, making rollups an attractive solution
for improving efficiency on platforms like Ethereum.

## ZK Rollups Vs Optimistic Rollups

Two primary types of rollups are utilized: ZK Rollups (Zero-Knowledge Rollups) and Optimistic Rollups.

### ZK Rollups

In ZK Rollups, the batch of transactions undergoes thorough verification for correctness on the main network. Successful
verification leads to the batch being treated as final, similar to a standard transaction. This verification relies on
cryptographic validity proofs, such as zero-knowledge proofs. Notable examples include [zkSync](../docs/zksync_era.md),
which employs a [zkSNARK](zkSNARK.md) for this process.

### Optimistic Rollups

Optimistic Rollups take a distinct approach by lacking a direct mechanism to prove the validity of off-chain
transactions. Operating on the assumption that off-chain transactions are valid unless proven otherwise, these rollups
rely on fraud-proof systems. Challenges to the submitted state trigger the need to demonstrate the validity of the
questioned state and transactions. Examples include Optimism and Arbitrum.
