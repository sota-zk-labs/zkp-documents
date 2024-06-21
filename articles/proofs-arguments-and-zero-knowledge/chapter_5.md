---
Title: Publicly Verifiable, Non-interactive Arguments via Fiat-Shamir
Status: Done
Level: "4"
comments: true
---

# Chapter 5 - Publicly Verifiable, Non-interactive Arguments via Fiat-Shamir

## 5.1 The Random Oracle Model (ROM)

You should read the definition of Random Oracle Model [here](../../terms/random_oracle_model.md)

## 5.2 The Fiat-Shamir Transformation

You should read the definition of Fiat-Shamir Transformation [here](../../terms/fiat_shamir.md)

## 5.3 Security of the Transformation

When the [Fiat-Shamir](../../terms/fiat_shamir.md) transformation is applied to a constant-round [IP](../../terms/ip.md) or
[argument](../../terms/arguments.md) $I$ with negligible soundness error, the resulting $Q$ in [ROM](../../random_oracle_model.md) is
sound against cheating provers
that run in polynomial time. Specifically, if an interactive proof $I$ for a [language](../../terms/language.md) $L$ satisfies a
property called [round-by-round soundness](../../terms/round_by_round_soundness) then $Q$ is sound in the
[ROM](../../random_oracle_model.md).

## 5.3.1 “Bits Of Security”: Statistical vs. Computational

In [chapter 4](chapter_4.md), we have seen that interactive protocols can satisfy statistical (i.e., information-theoretic) security.
The logarithm of the soundness error $(log(\delta _ s))$ of these protocols is the number of ==bits of statistical security==.

For non-interactive argument, the security level is measured by the amount of work that must be done to find a convincing “proof” of a
false statement. The logarithm of this amount of work is the number of ==bits of computational security==.

In many succinct interactive arguments, there are many properties that adversaries cannot break a cryptographic primitive (e.g.,
cannot find a collision in a collision-resistant hash function) and also cannot convince the verifier to accept a false statement with
probability more than $2^{-s}$. Here, $s$ is the number of ==bits of interactive security==.

**Appropriate security levels for interactive vs. non-interactive arguments.**

Non-interactive arguments are generally recommended to be deployed with at least $100$ or $128$ bits of computational security. In
contrast, it may be appropriate in some contexts to set statistical or interactive security levels lower.

For example, suppose that an [IP](../../terms/ip.md) runs at $60$ bits of interactive security, this means that each attempt attack
succeeds with a probability at most $2^{-60}$. So after $2^{30}$ attempt attacks, the probability that any of the attempts succeed is
at most $2^{-60} * 2^{30} = 2^{-30}$. The verifier, of course, will not continue interacting with a prover who has attempted attacks
$2^{30}$ times. Moreover, launching $2^{30}$ attacks takes a significant amount of time. So for [IP](../../terms/ip.md) in this
context, $60$ bits is sufficient.

In contrast, suppose that a non-interactive argument runs at $60$ bits of interactive security. So cheating prover only needs to try
about $2^{60}$ first messages before getting lucky. When applying [Fiat-Shamir](../../terms/fiat_shamir.md) transformation, the
computational bottleneck in this attack may be simply performing $2^{60}$ hash  
evaluations. However, in 2020, a bitcoin miners can perform $2^{80}$ **SHA-256** evaluations every 18 hours; hence, attacking in this
manner is entirely feasible for modern computers.

## 5.3.2 Soundness in the Random Oracle Model for Constant-Round Protocols

**Theorem 5.1**: Let $I$ be a constant-round [IP](../../terms/ip.md) or [argument](../../terms/arguments.md) with negligible soundness
error, and let $Q$ be the
non-interactive protocol in the [random oracle model](../../random_oracle_model.md) obtained by applying the
[Fiat-Shamir](../../terms/fiat_shamir.md) transformation to $I$. Then $Q$ has negligible computational soundness error. That is, no
prover running in polynomial time can convince the verifier in $Q$ of a false statement with non-negligible probability.

## 5.3.3 Fiat-Shamir Preserves Knowledge-Soundness in the Random Oracle Model

In [Section 7.4](chapter_7.md#7.4 Knowledge-Soundness), we will be concerned with a strengthening of soundness called
==knowledge-soundness== that is relevant
when the prover is claiming to know a witness satisfying a specified property.

In the [ROM](../../terms/random_oracle_model.md), the [Fiat-Shamir](../../terms/fiat_shamir.md) transformation preserves
knowledge-soundness. For example:

- [Section 9.2](chapter_9.md): Fiat-Shamir transformation preserves knowledge-soundness when apply to succinct arguments obtained
  from PCPs and IOPs.
- [Section 12.2](chapter12.md): The transformation is applied to $\sum$-protocols.

## Fiat-Shamir in the Plain Model

When the concrete hash function $h$ is chosen at random from a hash family $H$ satisfying
[CI](../../terms/correlation_intractability.md), instantiating the [Fiat-Shamir](../../terms/fiat_shamir.md) transformation in the
plain model results in a sound
argument.

### What is correlation-intractability (CI)?

You should read the definition [here](../../terms/correlation_intractability.md).

### Recent results constructing CI hash families

It is plausible that cryptographic hash families used in practice actually satisfy the relevant notions of
[correlation-intractability](../../terms/correlation_intractability.md).
