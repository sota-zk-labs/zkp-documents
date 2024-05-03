# Folding Scheme

Intuitively, a folding scheme for a [relation](../relation.md) $R$ is a protocol 
that reduces the task of checking two instances in $R$ to the task of 
checking a single instance in $R$.

For example, we want to compress two instances $x_1, x_2$ with witnesses $w_1, w_2$
to a single instance $x$ with witness $w$.

It meets both completeness and knowledge soundness requirements:
- If $w_1, w_2$ are correct, then the new witness $w$ is correct.
- If the new witness $w$ is correct for the folded instance $x$, then
the original witnesses $w _ 1, w _ 2$ for the initial instances 
$x _ 1, x _ 2$ can be extracted.