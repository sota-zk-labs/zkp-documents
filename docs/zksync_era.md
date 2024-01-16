# zkSync Era

## ZKP-Type

The zkSync Era combines [PLONK](plonk.md) and [FRI](fri.md) to create a powerful cryptographic construct known
as [zkSTARK](../terms/zkSTARK.md)

## zkSync Era Basics

In the zkSync Era, computational processes occur off-chain, accompanied by the storage of most data off-chain as well.
However, it's important to note that during this era, zkSync is currently centralized, solely operated by the zkSync
team's servers.

The lifecycle of zkSync [rollup](../terms/rollup.md) operations follows these stages:

1. A user initiates a transaction or a priority operation.
2. The operator processes the request, creating a rollup operation added to the block.
3. Upon completing the block, the operator submits it to the zkSync smart contract as a block commitment. Some rollup
   operations' logic is checked by the smart contract during this phase.
4. The proof for the block is submitted to the zkSync smart contract as block verification. If successful, the new state
   achieves finality.

Each L2 block progresses through four stages until it reaches finality:

- **Pending:** The operator received the transaction but has not processed it yet.
- **Processed:** The operator processes the transaction, confirming its inclusion in the next block.
- **Committed:** Transaction data for this block is posted on Ethereum, ensuring data availability.
- **Finalized:** The SNARK validity proof for the transaction is submitted and verified by the smart contract, marking
  the transaction as final.

### Noteworthy Features of zkSync Era

- Mainnet-like security without reliance on third parties.
- Permissionless EVM-compatible smart contracts.
- Standard Web3 API.
- Preservation of key EVM features, including smart contract composability.
- Introduction of new features, such as account abstraction.
