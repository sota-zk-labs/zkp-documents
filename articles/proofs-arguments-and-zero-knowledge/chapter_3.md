---
Title: Definitions and Technical Preliminaries
Status: Done
Level: "3"
---

# Chapter3 - Definitions and Technical Preliminaries

## 3.1 Interactive Proofs

Prover (**P**) claims that he has a value y = f(x). To verify it, verifier (**V**) exchanges messages with **P** back
and forth. At the end of this protocol, **V** must output either 0 or 1, with 1 indicating that the verifiers accept the
prover’s claim that y = f(x) and 0 indicating that the verifier rejects the claim.
The entire sequence of k messages $t := (m_1,m_2,...,m_k)$ exchanged by $P$ and $V$, along with the claimed answer y, is
called a ==transcript==.

$Out(V,x,r,P) ∈ \{0,1\}$ the output of verifier $V$ on input $x$ when interacting with deterministic prover strategy P,
with V’s internal randomness equal to r.

An interactive proof system (V,P) is said to have completeness error $δ_c$ and soundness error $δ_s$ :

- [Completeness](../../terms/zkp#completeness)   error $δ_c$ :        $\text{Pr}[\text{out}(V, x, r, P) = 1]$ $\ge$ 1 -
  $δ_c$
- [Soundness](../../terms/zkp.md#soundness) error $δ_s$:              $\text{Pr}[\text{out}(V, x, r, P') = 1]$ $\le$
  $δ_s$, which $P'$ is prover strategy with value: $y \ne f(x)$(*statistical soundness*).

An interactive proof system is valid if $δ_c$ , $δ_s$ ≤ 1/3.

## 3.2 Argument Systems

**Definition**: read [here](../../terms/arguments.md)

## 3.3 Robustness of Definitions and the Power of Interaction

- Any [IP](../../terms/ip.md) for a function $f$ with $δ_c$ ≤ 1/3 can be transformed into perfect completeness ($δ_c$ =
  0), with a polynomial blowup in the verifier’s costs.
- Soundness Error:  $1 / |F|$ , where $F$ is the field over which the interactive proof is defined.

**Interactive Proofs for Languages Versus Functions.**

The standard requirements of an IP for the [language](../../terms/language.md) $L$ are:

- Completeness: For any $x \in L$, there are some prover strategies that will cause the verifier to accept with high
  probability.
- Soundness: For any $x \notin L$, then for every prover strategy, the verifier rejects with high probability.

The above properties do not require that *false statement*s (which inputs not in the language) have convincing
refutations (i.e., convincing proofs of their falsity)

**NP and IP**
You should read the definitions here: [IP](../../terms/ip.md) and [NP](../../terms/np.md) .

## 3.4 Schwartz-Zippel Lemma

You should read this lemma [here](../../terms/schwartz_zippel_lemma.md)

## 3.5 Low Degree and Multilinear Extensions

You should read the definitions of [Multilinear](../../terms/multilinear.md) and [Extension](../../terms/extension)

**Fact 3.5**:  Any function $f: \{0, 1\}^v → F$ has a unique multilinear extension (MLE) over $F$.
You can read the proof here: [Uniqueness of Multilinear Extension](../../terms/uniqueness_of_multilinear_extension.md).

We reserve the notation $\tilde{f}$ for this special extension of $f$
$$\tilde{f}(x_1, ..., x_v) = \sum_{w\in \{0,1\}^v} f(w)· χ_w(x_1, ..., x_v), $$
where, for any $w = (w1,...w_v)$ : $$χ_w(x_1,...,x_v) := \prod_{i=1}^v (x_iw_i + (1 - x_i)(1-w_i)). $$
The set $\{χ_w: w \in \{0, 1\}^v\}$ is referred to as the set of ==*multilinear Lagrange basis polynomials*==.

### Evaluating the multilinear extension of f

There are two efficient methods for evaluating $\tilde f$ at any point of $r \in F^v$.

The first one is **CTY11**: Fix a positive integer $v$ and let $n = 2^v$. Given as input $f(w)$ for all $w \in \{0,
1\}^v$ and a vector $r \in F^{log n}$, $V$ can compute $\tilde f(r)$ in O($nlogn$) time and O($logn$) space.

### Proof

$V$ can compute $\tilde f(r)$ incrementally from the stream: $\tilde f(r) ← \tilde f(r) + f(w) · χ_w(r)$
So, $V$ needs to store $\tilde f(r)$ and $r$, which requires O($log n$) space.

The second one is **VSBW13**: $V$ can compute $\tilde f(r)$ in O($n$) time and O($n$) space.

#### Proof

$\tilde f(r)$ can be expressed as the inner product of 2 $n$-dimensional vectors, where $w$-th entry of them are $f(w)$
and $χ_w(r)$ respectively. To compute this in O($n$) with O($n$) space, we create $v$ stages, where $j$-th stage
constructs a table $A^{(j)}$ of size $2^j$:
For any $(w_1,...w_j)$, we have $$A^{(j)}[(w_1,...,w_j)]=\prod_{i = 1}^jχ_{w_i}(r_i)$$
So we have the following dynamic programming formula: $$A^{(j)}[(w_1,...,w_j)]=A^{(j - 1)} [(w_1,...,w_{j - 1})]·(
w_jr_j + (1 - w_j)(1-r_j)$$
So, this stage requires time O($2^j$). Total time is: $$\text O(\sum_{j=1}^{logn}2^j) = \text O(2^{logn}) = \text O(
n)$$.
