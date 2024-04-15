# Chinese Remainder Theorem

Let us denote:
- $n_i > 1 \ \forall i = 1,2,...,k$  and they are pairwise coprime.
- $a_1, a_2,...,a_k$ are any integers
- $N = \prod\limits_{i=1}^{k}{n_i}$

then the system


$$
\begin{aligned}
x \equiv a_1 & \pmod{n_1} \\
&... \\
x \equiv a_k & \pmod{n_k}
\end{aligned}
$$


has only one solution $x$ s.t. $x < N$

To find $x$, we need more notations:
- $N_i = \dfrac{N}{n_i}$
- $inv_i$ such that $inv_i \cdot N_i \equiv 1 \pmod{n_i}$

then $x \equiv \sum{N_i \cdot inv_i \cdot a_i} \pmod{N}$ 

For example, with $k = 3$ and:
- $n = \lbrace5, 7, 11\rbrace$
- $a = \lbrace 2, 3, 4\rbrace$
- $N = \prod\limits_{i=1}^{k}{n_i} = 5 * 7 * 11 = 385$

So:
- $N_1=77, N_2=55,N_{3}=35$
- $inv_{1}=3, inv_{2}=6, inv_{3}=6$

Finally, $x=77 * 3 * 2 + 55 * 6 * 3 + 35 * 6 * 4 \mod 385 = 367$. As expected, we have:
- $367 \equiv 2 \pmod{5}$
- $367 \equiv 3 \pmod{7}$
- $367 \equiv 4 \pmod{11}$ 