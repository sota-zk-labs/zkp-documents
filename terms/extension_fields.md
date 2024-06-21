---
comments: true
---

# Extension Fields

## Definition

Let $i = \sqrt{-1}$.

Extension fields function by introducing a new element and defining its relationship with existing elements in the
field (in this case, $i^2 + 1 = 0$) (also referred to as a [Quadratic field](quadratic_field.md)).

## Extensions of Finite Fields

Standard operations apply, with the exception of division:

$a / b = (a \cdot b^{p^{2}-2}) \pmod {p}$

$x^{p^2 - 1} \equiv 1 \pmod p$ => $p^2 - 1$ is the [**order of the multiplicative group in the field
**](prime_or_finite_fields.md#order-of-the-multiplicative-group)

### Examples

Consider extending the prime field modulo 7 with $i$:

- $(2 + 3i) + (4 + 2i) = 6 + 5i$
- $(5 + 2i) + 3 = 1 + 2i$
- $(6 + 2i) \cdot 2 = 5 + 4i$
- $4i \cdot (2 + i) = 3 + i$

However, the result of $(2 + 3i) / (4 + 2i)$ may be a bit challenging to understand. Here's the breakdown: we first
decompose the product into $4i \cdot 2 + 4i \cdot i$, yielding $8i - 4$. Since we're working in modulo 7 arithmetic,
this simplifies to $i + 3$.
