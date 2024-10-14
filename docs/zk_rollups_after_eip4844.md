---
cards-deck: docs
---
# ZK-Rollups after EIP-4844

**References:**

- [EIP-4844 Homepage](https://www.eip4844.com/#help-out)
- [How to use KZG commitments in proofs](https://notes.ethereum.org/@dankrad/kzg_commitments_in_proofs)
- [Data Availability Post 4844](https://scroll.io/blog/data-availability-4844)

## Introduction []()

**EIP-4844** (or Proto-Danksharding) is the backbone of the Ethereum Dencun upgrade. This upgrade focuses on Layer 2 scalability by
introducing blob transactions and blob data, resulting in significantly reduced storage costs and gas fees.

Here are a few important points of EIP-4844 from ZK-Rollups' perspective:

- Data can now be stored in blobs, which contain $4096$ chunks of $32$ bytes each.
- The execution layer (which can be understood as similar to smart contract) only can access
  to the [versioned hashes](https://eips.ethereum.org/EIPS/eip-4844#helpers)
  of the [KZG commitments](../terms/polynomial-commitment/100_kate_commitment.md) of data in the blobs.
- The KZG commitment will be automatically calculated, and we can use the `blobhash` opcode to get the versioned hash to verify the
  commitment.
- [BLS12-381](../terms/bls12-381.md) modulus is used in the KZG commitment.
- The reason we couldn't simply generate a commitment by hashing the data blob is because we can't prove any properties of
  the data blob without revealing the whole thing.

[](1724550257021)

## KZG Commitments of Blob Data []()

The function $f$ is defined as the Lagrange polynomial:

$$
\begin{aligned}
f(\omega^i) = d_i
\end{aligned}
$$

where $\omega^{4096} = 1$ is a [root of unity](plonk.md#Roots%20of%20Unity) of order $4096$, and $d_i$ define the data points in blob.
This function is then committed using KZG.

[](1724550257036)

## Point Evaluation Precompile []()

The EIP4844 introduces a new precompile at `Bytes20(0x0A)` that is designed to allow users to open the commitment to a blob. Below is
the pseudocode copied from [EIP-4844 specs](https://eips.ethereum.org/EIPS/eip-4844).

```python
def point_evaluation_precompile(input: Bytes) -> Bytes:
    """
    Verify p(z) = y given commitment that corresponds to the polynomial p(x) and a KZG proof.
    Also verify that the provided commitment matches the provided versioned_hash.
    """
    [](1724550257039)

# The data is encoded as follows: versioned_hash | z | y | commitment | proof | with z and y being padded 32 byte big endian values
    assert len(input) == 192
    versioned_hash = input[:32]
    z = input[32:64]
    y = input[64:96]
    commitment = input[96:144]
    proof = input[144:192]

    # Verify commitment matches versioned_hash
    assert kzg_to_versioned_hash(commitment) == versioned_hash

    # Verify KZG proof with z and y in big endian format
    assert verify_kzg_proof(commitment, z, y, proof)

    # Return FIELD_ELEMENTS_PER_BLOB and BLS_MODULUS as padded 32 byte big endian values
    return Bytes(U256(FIELD_ELEMENTS_PER_BLOB).to_be_bytes32() + U256(BLS_MODULUS).to_be_bytes32())


def kzg_to_versioned_hash(commitment: KZGCommitment) -> VersionedHash:
    return VERSIONED_HASH_VERSION_KZG + sha256(commitment)[1:]
```

The `point_evaluation_precompile(versioned_hash, z, y, kzg_commitment, proof)` receives a versioned hash, the KZG commitment to the
blob, and a KZG opening proof for point $z$ and value $y$ as input. It verifies that `kzg_commitment` corresponds to
the `versioned_hash` provided and that the opening `proof` is valid (i.e. $f(z)=y$).

## Blob Consistency Check []()

Since rollup contract only can access to versioned hash instead of the raw transaction data (which was previously included
as `calldata`), the main challenge we face is proving that $f$ indeed ==represents exactly the raw transaction data using circuits==.
That is, we need to prove that our internal commitment scheme and KZG **commit to the same function** $f$ (can be called proof of
equivalence).
There is an easy approach in
the case where the ZK rollup is BLS12-381 based, and a moderately harder approach for arbitrary ZK-SNARKs.

[](1724550257042)

[](1724550257044)

### With BLS12-381 Modulus []()

Given two polynomial commitments $C_1$ and $C_2$ over the same field (but not the same scheme, e.g. they could be KZG and FRI, or both
KZG but with different trusted setup), here is the protocol:

1. Let $x = hash(C_1, C_2)$ (based on [Fiat-Shamir heuristic](../terms/fiat_shamir.md))
2. Compute $y = f(x)$
3. Generate proof $\pi_1$, that proves $y = f(x)$ with respect to $C_1$
4. Generate proof $\pi_2$, that proves $y = f(x)$ with respect to $C_2$

The prover sends $C_1,C_2,y,\pi_1, \pi_2$. The verifier accepts if $y = f(hash(C_1,C_2))$ and the proofs $\pi_1$ and $\pi_2$ verify.
This technique was summarized by
Vitalik [here](https://ethresear.ch/t/easy-proof-of-equivalence-between-multiple-polynomial-commitment-schemes-to-the-same-data/8188).

[](1724550257046)

### With Any ZK-SNARKs

We also choose $x$ as in previous section, and evaluate [barycentric equation](../terms/barycentric_equation.md) $f(x) = \dfrac{x^N}{N}\cdot \sum_{i}{\dfrac{d_i \cdot \omega^i}{x - \omega^i}}$ at our random $x$. This evaluation has to be done over BLS12-381 in our
circuit using [non-native field arithmetic](non_native_field_arithmetic.md).

#### Proof of Concept

[Here](https://github.com/mmjahanara/blob-consistency-check) is a PoC that implemented by Scroll. This implementation uses the `BN254`
modulus as native field, barycentric equation, along with non-native field arithmetic from Halo2's crates to create the circuit.

## How To Send Blob Transactions []()

To embed your data into a blob, you must convert it into `byte` format and use `kzg4844.Blob` to store it (`kzg4844.Blob` is
essentially `[131072]byte`). Then, calculate the KZG commitment and KZG proof to create a sidecar from these values.

```Go
import (
 "github.com/ethereum/go-ethereum/core/types",
 "github.com/ethereum/go-ethereum/crypto/kzg4844"
)

var Blob kzg4844.Blob
// Embed your data into the blob here


// Compute the commitment for the blob data using KZG4844
BlobCommitment, err := kzg4844.BlobToCommitment(Blob)

// Compute the proof for the blob data, which will be used to verify the transaction
BlobProof, err := kzg4844.ComputeBlobProof(Blob, BlobCommitment)

// Prepare the sidecar data for the transaction, which includes the blob and its cryptographic proof
sidecar := types.BlobTxSidecar{
  Blobs: []kzg4844.Blob{Blob},
  Commitments: []kzg4844.Commitment{BlobCommitment},
  Proofs: []kzg4844.Proof{BlobProof},
}
```

Finally, send the transaction.

```Go
txData = &types.BlobTx{
    /// another fields
    BlobHashes: sidecar.BlobHashes(),
    Sidecar:    sidecar,
}
// sign and send
signedTx, err := TransactOpts.Signer(fromAddress, types.NewTx(txData))
err = ethclient.Client.SendTransaction(context, signedTx)
```

The pseudocode above is for illustration purposes only. [Here](https://www.rareskills.io/post/ethclient-golang) is a more complete
implementation.

[](1724550257047)

### How To Verify The Commitment []()

Assume that in the `verify` function, we want to check whether the parameter `blobKZGProof` is consistent with the underlying blob. We
can first use the `blobhash` opcode to get the versioned hash of the blob, then use `point_evaluation_precompile()` to verify the
consistency as shown below.

```Solidity
/// Memory layout of `blobKZGProof`:
/// | z       | y       | kzg_commitment | kzg_proof |
/// |---------|---------|----------------|-----------|
/// | bytes32 | bytes32 | bytes48        | bytes48   |
function verify(
    bytes calldata blobKZGProof
) external {
    // Calculate the versioned hash of blobs[0]
    bytes32 _blobVersionedHash = blobhash(0);

    // Call the point evaluation precompile to ensure that `blobKZGProof` corresponds to the blob data.
    {
        (bool success, bytes memory data) = POINT_EVALUATION_PRECOMPILE_ADDR.staticcall(
            abi.encodePacked(_blobVersionedHash, blobKZGProof)
        );
        // Verify that the point evaluation precompile call was successful by testing that the latter 32 bytes of the
        // response are equal to BLS_MODULUS as defined in https://eips.ethereum.org/EIPS/eip-4844#point-evaluation-precompile
        if (!success) revert ErrorCallPointEvaluationPrecompileFailed();
        (, uint256 result) = abi.decode(data, (uint256, uint256));
        if (result != BLS_MODULUS) revert ErrorUnexpectedPointEvaluationPrecompileOutput();
    }
}
```

After this, you can start verifying the blob consistency check.

[](1724550257048)
