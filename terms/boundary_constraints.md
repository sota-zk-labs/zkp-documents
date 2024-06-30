---
comments: true
---
# Boundary Constraints

Boundary constraints specify that at any designated point within a computation, a particular register must hold a specified value.
We define  boundary constraints as a set $B$ of triple $(r, c, e) \in \lbrace0,..,T \rbrace \times \lbrace 0,...,w-1 \rbrace \times F$,
which means that the value of row $r$ and column $c$ is $e$ in trace.
