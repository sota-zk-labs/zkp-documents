# Chip

Provides efficient pre-built implementation of a particular functionality.

For example, we might have chips that implement particular cryptographic primitives such as a hash function or cipher, or algorithms
like scalar multiplication or pairings.

We define chips that "know" how to use particular sets of [custom gates](gate.md). This creates an abstraction layer that isolates the
implementation of a high-level circuit from the complexity of using custom gates directly.
