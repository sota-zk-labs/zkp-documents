# Sum-check Protocol

Given a $v$-variate polynomial $g$ defined over a finite field $F$. The purpose of the sum-check protocol is for the prover to provide
this sum for the verifier: $$H := \sum_{b_{1} \in \{0, 1\}} ... \sum_{b_{v} \in \{0, 1\}} g(b_{1},...,b_v)$$
**What does the verifier gain by using the sum-check protocol ?**
Instead of compute $H$ via the equation above (runtime $2^v$), $V$ can use sum-check protocol to reduce runtime to:
$O(v + \text{the cost to evaluate }g \text{ at a single input in }F^v)$. $P$ can compute all of its prescribed messages by evaluating
$g$ at $O(2^v)$ inputs in $F^v$.

**Description of Sum-Check Protocol**

1. At the start of the protocol, the prover sends a value $C_1$ claimed to equal the value $H$ defined in the equation above.
2. In the first round, $P$ sends the univariate polynomial $g_1(X_1)$ claimed to equal:
$$\sum_{(x_2,..,x_v) \in \{0, 1\}^{v-1}} g(X_1, x_2,...,x_v)$$
   $V$ checks that :
   - $g_1(0) + g_1(1) = C_1$
   - $g_1$ is a univariate polynomial of degree at most $deg_1(g)$ where  $deg_j(g)$ is the degree of $g(X_1, X_2,.. X_v)$ in variable
   $X_j$.

3. $V$ chooses a random element $r_1 \in F$, and sends $r_1$ to $P$
4. In the $j$-th round, for $1 < j < v$, $P$ sends to $V$ a univariate polynomial $g_j(X_j)$ claimed to equal:
$$\sum_{(x_{j+1},..,x_v) \in \{0, 1\}^{v-j}} g(r_1,...,r_{j-1},X_j,x_{j+1}...,x_v)$$
   $V$ checks that:
   - $g_j(0) + g_j(1) = g_{j-1}(r_{j-1})$
   - $g_j$ is a univariate polynomial of degree at most $deg_j(g)$.
   Rejecting if not.
5. $V$ chooses a random element $r_j \in F$, and sends it to $P$.
6. In Round $v$, after $P$ sends $g_v(X_v)$ to $V$ and $V$ check the conditions, $V$ chooses a random element $r_v \in F$, evaluates
$g(r_1, r_2,...,r_v)$ and checks that $g_v(r_v) = g(r_1,...,r_v)$, rejecting if not.
7. If $V$ has not yet rejected, $V$ accepts.

**Completeness and Soundness**
Let $g$ be a $v$-variate polynomial of degree at most $d$ in each variable, defined over a finite field $F$, the completeness error
$\delta_c = 0$ and the soundness error $\delta_s \le vd/|F|$

**Discussion of costs**

| Communication | Round | $V$ time | $P$ time |
| ---- | ---- | ---- | ---- |
| $O(\sum_{i=1}^v deg_i(g))$ | $v$ | $O(v+\sum_{i=1}^v deg_i(g)) + T$ | $O(\sum_{i=1}^v deg_i(g)\cdot 2^{v-i}\cdot T)$  |

where $T$ is the cost of an oracle query to $g$.
