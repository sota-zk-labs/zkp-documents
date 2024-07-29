## HMAC

This definition is taken from [RFC 2104](https://datatracker.ietf.org/doc/html/rfc2104):

$$
\begin{align}
\operatorname{HMAC}(K, m) &= \operatorname{H}\Bigl(\bigl(K' \oplus opad\bigr) \parallel  
\operatorname{H} \bigl(\left(K' \oplus ipad\right) \parallel m\bigr)\Bigr) \\  
K' &= \begin{cases}  
\operatorname{H}\left(K\right) & \text{if}\ K\text{ is larger than block size} \\  
K & \text{otherwise}  
\end{cases}  
\end{align}
$$

where:

- `H` is a cryptographic hash function.
- `m` is the message to be authenticated.
- `K` is the secret key.
- `K'` is a block-sized key derived from the secret key, either by padding to the right with 0s up to the block size, or by hashing down to less than or equal to the block size first and then padding to the right with zeros.
- $\parallel$ denotes `concatenation`.
- $\oplus$ denotes bitwise `exclusive or` (XOR).
- `opad` is the block-sized outer padding, consisting of repeated bytes valued `0x5c`.
- `ipad` is the block-sized inner padding, consisting of repeated bytes valued `0x36`.

## GSW Homomorphic Commitment Scheme

[View this for details](docs/gsw_fhe_scheme.md)

# The Solution

## Setup Phase (performed by a trusted party)

1. **Prepare for the GSW Commitment Scheme:**
   - Generate a uniformly random matrix $A$ needed in both the commitment and verification phases.

2. **Generate Commitments for the `bot_token`:**
   - First, calculate:
     $$
     \{b = \text{Sha256}(\operatorname{bot\_token})\} \in \{0, 1\}^{256}
     $$
     where $b$ is the binary form of the hash value of the `bot_token`.
   - Then, commit each bit of $b$:
     $$
     \{cb_i, rb_i\} = \operatorname{Commit}(A, b_i); \forall i \in \{1, 2, \ldots, 256\}
     $$
     where $cb_i = A \times rb_i + b_i \times G$, with $G$ being the gadget matrix.
   - Prepare two more commitments for bit $0$ and bit $1$:
     $$
     \{c0, r0\} = \operatorname{Commit}(A, 0)
     $$
     $$
     \{c1, r1\} = \operatorname{Commit}(A, 1)
     $$
   - Finally, publish $c0, r0, c1, r1, A, \{c_i, r_i\}; \forall i \in \{1, 2, \ldots, 256\}$.

## Proving Phase

1. **User Authentication and Information Commitment:**
   - After successful authentication, Telegram provides the prover with user info, including _id_, _first_name_, _last_name_, _username_, _photo_url_, and _auth_date_ fields:
     $$
     \operatorname{info} = \{0,1\}^n
     $$
     where $n$ is the bit-length of the info, and:
     $$
     sig = \operatorname{Hmac}(\text{bot\_token}, \operatorname{info}) = \{0, 1\}^{256}
     $$
   - The prover then commits to the $\operatorname{user\_info}$ by mapping each bit of the user info with the commitment already published:
     $$
     \{cu_i, ru_i\} =
     \begin{cases}
     \{c0, r0\} & \text{if info}_i = 0 \\
     \{c1, r1\} & \text{if info}_i = 1
     \end{cases}; \forall i \in \{1, 2, \ldots, n\}
     $$
2. **Opening Computation:**
   - Assume there exists an algorithm $\operatorname{Open}()$ that, without knowing the $\text{bot\_token}$, can compute the opening $r_i$ for each output of 256 bits (using the "Input-dependent Evaluation" technique). The prover calculates:
     $$
     r = \{r_i; \forall i \in \{1, 2, \ldots, 256\} \} = \operatorname{Open}(ru, rb, \text{info})
     $$
   - The prover then sends $cu, r, \text{info}, \text{sig}$ to the verifier.

## Verification Phase

1. **Hmac Commitment Computation:**
   - The verifier computes the "Hmac" commitment $c$ using the "Input-Independent Evaluation" technique:
     $$
     c = \{c_i; \forall i \in \{1, 2, \ldots, 256\} \} = Hmac_e(cu, cb)
     $$
     where $Hmac_e$ is an equivalence algorithm to compute Hmac on the committed commitments.
2. **Commitment Check:**
   - The verifier checks whether:
     $$
     c_i \stackrel{?}{=} A \times r_i + \text{sig}_i \times G; \forall i \in \{1, 2, \ldots, 256\}
     $$
   - The verifier then checks the consistency of the user's info:
     $$
     cu_i \stackrel{?}{=}
     \begin{cases}
     c0 & \text{if info}_i = 0 \\
     c1 & \text{if info}_i = 1
     \end{cases}; \forall i \in \{1, 2, \ldots, n\}
     $$

## End Result

If all the checks return `true`, the verifier can determine that the user is valid without knowing the plain `bot_token`. After the setup phase, only Telegram and the bot owner know the plain `bot_token` value, ensuring that no one else can create a valid fake proof.

## Problems with Our Solution

Designing the desired $\operatorname{Open}$ function involves dealing with two operations ($+$) and ($\times$) without knowing the underlying message. Currently, we can only do this for the ($+$) operation, making this solution impractical.

## Conclusion

Using this strategy does not seem feasible for now.

## Alternative Solution

A viable solution is to deploy an intermediate service that receives `user_hash` from users and then returns a new JWT token corresponding to the user's request. The flow would then be the same as the one we have deployed.
