---
comments: true
---

# Round-by-round Soundness

A protocol $I$ for a [language](language.md) $L$ satisfies round-by-round soundness if the following properties hold:

- At any stage of any execution of $I$, there is a well-defined state and some states are "doomed". Once the protocol $I$ is in a
  doomed state, it will (except with negligible probability) forever remain doomed.
- If $x \notin L$ then the initial state is doomed.
- If at the end of the interaction the state is doomed, then the verifier will reject.

Canetti et al.[CHH+19](https://dl.acm.org/doi/10.1145/3313276.3316380) showed that any interactive proof based on
[sum-check protocol](sumcheck_protocol.md) satisfy round-by-round soundness, and hence applying the [Fiat-Shamir](fiat_shamir.md)
transformation to it yields a [non-interactive proof](np.md) that is secure in the [ROM](random_oracle_model.md).
