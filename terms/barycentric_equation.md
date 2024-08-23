---
comments: true
cards-deck: terms
---

# Barycentric Equation []()

For a given set of pairs $(x_1;y_1), (x_2; y_2), ..., (x_N; y_N)$, let $P(x)$ be the polynomial such that $P(x_i) = y_i  \forall i=1,...,N$. Usually, to evaluate $P(x)$ at an arbitrary point, we can interpolate $P(x)$
using [Lagrange interpolation](lagrange_interpolation.md) in $O(N^2)$ time in general case, and in $O(Nlog_2N)$ in special cases.
Alternatively, utilizing the barycentric formula allows for direct evaluation of $P(x)$ in $O(N)$ time, with pre-computed time
complexity of $O(N^2)$ in the general case. For example, if $P(x)$ is a degree-100 polynomial, you can use the evaluations
$P(0), P(1), ..., P(100)$ to compute $P(101)$, or $P(12042003)$, without ever reconstructing the polynomial.

[](1724425326555)

## General Technique

From Lagrange interpolation, we have $P(x) = \sum_{i}{y_i L_i(x)}$. Let us denote:

- $d_i=\prod_{j \neq i}{(x_i - x_j)}$
- $M(x) = \prod_{i}{x-x_i}$

We can now express $L_i(x)$ as $\dfrac{M(x)}{d_i(x-x_i)}$ for $(x \neq x_i)$. It takes $O(N^2)$ time to compute all $d_i$, $O(N)$ time
for $M(x)$ and $L_i(x)$. Hence, the expression:

$$
P(x) = M(x) * \sum_{i}{\frac{y_i}{d_i(x-x_i)}}
$$

can be computed in $O(N)$ time if we cache the results of $d_i$.

## Special Case: Roots of Unity

In case our points are $1, \omega, \omega^2, ..., \omega^{N-1}$ where $\omega^N = 1$ is a [root of unity](plonk.md#Roots%20of%20Unity)
and $N$ is a **power of two**, we don't need to pre-compute the $d_i$ anymore. We can rewrite $d_i$ as follows:

$$
d_i = \prod_{0 \leq j \neq i < N}{(\omega^i - \omega^j)}
$$

Notice that $\omega^{\frac{N}{2}} = -1$. We can re-express the above as:

$$
\begin{aligned}
d_i & = (\omega^i - \omega^{i + \frac{N}{2}}) * \prod_{0 \leq j \neq i < \frac{N}{2}}{(\omega^i-\omega^j)(
\omega^i-\omega^{j+\frac{N}{2}})} \\ \\
& = 2\omega^i * \prod_{0 \leq j \neq i < \frac{N}{2}}{(\omega^{2i}-\omega^{2j})}
\end{aligned}
$$

Repeat this, and we have:

$$
d_i = 2\omega^i * 2\omega^{2i} * \prod_{0 \leq j \neq i < \frac{N}{4}}{(\omega^{4i}-\omega^{4j})}
$$

Keep repeating, and we get:

$$
\begin{aligned}
d_i & = 2\omega^i * 2\omega^{2i} * 2\omega^{4i} * ... * 2\omega^{\frac{N}{2}i} \\ \\
&= 2^{log_2(N)} * \omega^{(1+2+...+\frac{N}{2})i} \\ \\
&= N * \omega^{(N-1)i}\\ \\
&= \frac{N}{\omega^i}
\end{aligned}
$$

Additionally, note that $M(x)=\prod_{i}{x - \omega^i}$ simply becomes $x^N-1$, so the entire calculation simplifies down to:

$$
P(x) = \frac{x^N-1}{N} * \sum_{i}{\frac{y_i * \omega^i}{x-\omega^i}}
$$

**References:**

- [A quick barycentric evaluation tutorial](https://hackmd.io/@vbuterin/barycentric_evaluation)
