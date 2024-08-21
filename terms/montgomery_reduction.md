---
comments: true
---
# Montgomery Reduction

This is an efficient method for computing $R = a \cdot b \mod n$ where $a, b, \text{and } n$ are $k$-bit binary number. For our
purposes, we suppose that $n$ is an odd number.

## Preliminaries

First, we choose $r > n$ such that: $(r, n) = 1$. Because $n$ is odd, we often choose $r = 2^k$.

This technique replaces division by $n$ with division by a power of $2$, , which is easily performed on a computer since numbers are
represented in binary form.

To achieve this, we need to convert all the numbers we use into Montgomery space. The $n$-residue of $a$ in Montgomery space is given
by:
$\bar a = a \cdot r \mod n$

## Montgomery Multiplication

The Montgomery product is defined as:
$\bar R = \bar a \cdot \bar b \cdot r^{-1} \mod n$, which represents the $n$-residue of $R = a \cdot b \mod n$.

To compute this product, we need to determine $r^{-1}$, which satisfies the property:  

$r \cdot r^{-1} = 1 \mod n$
$\iff r \cdot r^{-1} - n \cdot n' = 1$ where $n'$ is a $k$-bit binary number.

Therefore, we can find $r^{-1}$ and $n'$ using the
[Extended Euclid algorithm](https://en.wikipedia.org/wiki/Extended_Euclidean_algorithm). We can express $\bar{R}$ as follows:

$\bar R = \bar a \cdot \bar b \cdot r^{-1} \mod n$
$= (\bar a \cdot \bar b \cdot r^{-1} \cdot r) / r  \mod n$
$=  (\bar a \cdot \bar b) \cdot (1 + n \cdot n') / r \mod n$
$=  (\bar a \cdot \bar b + (\bar a \cdot \bar b) \cdot n \cdot n') / r \mod n$

The computation of the Montgomery product is as follows:

**The Montgomery product function:**

```bash
function MonPro(¯a, ¯b) 
Step 1. t := ¯a · ¯b mod r 
Step 2. m := t · n' mod r 
Step 3. u := (¯a · ¯b + m · n)/r 
Step 4. if u ≥ n then return u − n else return u
```

**The ModMul ($a \cdot b \mod n$) function:**

```bash
function ModMul(a, b, n) { n is an odd number } 
Step 1. Compute n' using the extended Euclid algorithm. (can be computed in preparation) 
Step 2. ¯a := a · r mod n 
Step 3. ¯b := b · r mod n 
Step 4. ¯x := MonPro(¯a, ¯b) 
Step 5. x := MonPro(¯x, 1) 
Step 6. return x
```

We convert $\bar x$ to $x$ by invoking `MonPro(¯x, 1)`. This shown to be correct since:
$\bar x = x \cdot r \mod n \iff x = \bar x \cdot r^{-1} \mod n$
$= \bar x \cdot 1 \cdot r^-1 \mod n$
$= MonPro(\bar x, 1)$

> [!NOTE]
> Because the pre-processing operations (conversion to $n$-residue, computation of $n'$, and converting the result back to ordinary
> residue) are time-consuming, it is not good to use Montgomery product when performing single modular multiplication

**Fast Transform**:

We notice that transforming $\bar x$ from $x$ can be computed more efficiently than directly evaluating  $\bar x = x \cdot r \mod n$.

Specifically, have $$\bar x = x \cdot r = x \cdot r^2 \cdot r^{-1} = x * r^2$$

Transforming a number into the space is just a multiplication inside the space of the number with $r^2$. This allows us to precompute
$r^2 \bmod n$ and perform a multiplication.

For example, let $x = 9, r = 16$ and $n = 13$. Then $n' = 11, r^{-1} = 9$ (computed using Extended Euclid algorithm).

Using the original method: $\bar x = 9 * 16 \mod 13 = 1$.

Using fast transform:

- Precompute: $r^2 \mod n = 16^2 \mod 13 = 9$
- Compute: $\bar x = MonPro(x, r^2) = MonPro(9, 9) = 1$.

### Example

We show how to compute $9 * 11 \mod 13$ ($= 8$). We have:

- $r = 2^4 = 16$
- Using the Extended Euclid algorithm, we determine that $16 * 9 − 13 * 11 = 1$, thus, $r^{-1} = 9, n' = 11$

We invoke the `ModMul` function:

- $\bar a = 9 * 16 \mod 13 = 1$
- $\bar b = 11 * 16 \mod 13 = 7$
- $\bar x = \text{MonPro}(1, 7) = 11$
- $x = \text{MonPro}(11,1) = 8$

$\text{MonPro}(1, 7):$

- $t = 1 * 7 \mod 16 = 7$
- $m = 7 * 11 \mod 16 = 13$
- $u = (1 * 7 + 13 * 13) / 16  = 11$
- return $11$

$\text{MonPro}(11, 1)$:

- $t = 11 * 1 \mod 16 = 11$
- $m = 11 * 11 \mod 16 = 9$
- $u = (11 * 1 + 9 * 13)/16 = 8$
- return $8$

## Montgomery Exponentiation

We want to compute $a^e \mod n$. First, we replace the exponentiation operation by a series of square and multiplication operations
modulo $n$. Then, we replace the multiplication by Montgomery `MonPro()`.

```bash
function ModExp(a, e, n) { a^e mod n, n is an odd number }
Step 1. Compute n' using the extended Euclid algorithm.(can be computed in preparation)  
Step 2. ¯a := a · r mod n 
Step 3. ¯x := 1 · r mod n 
Step 4. for i = k − 1 down to 0 do 
Step 5.     ¯x := MonPro(¯x, x¯) 
Step 6.      if e_i = 1 then x¯ := MonPro(¯a, x¯) 
Step 7. x := MonPro(¯x, 1) 
Step 8. return x
```

### Example

We show how to compute $x = 7^{10} \mod 13$ ($=4$). We have:

- $r = 2^4 = 16$
- Using the Extended Euclid algorithm, we determine that $16 * 9 − 13 * 11 = 1$, thus, $r^{-1} = 9, n' = 11$

We invoke `ModExp` function:

- $\bar a = 7 * 16 \mod 13 = 8$
- $\bar x = 1 * 16 \mod 13 = 3$
- Step $5$ and $6$:

| $e_i$ | Step 5            | Step 6           |
| ----- | ----------------- | ---------------- |
| 1     | MonPro(3, 3) = 3  | MonPro(8, 3) = 8 |
| 0     | MonPro(8, 8) = 4  |                  |
| 1     | MonPro(4, 4) = 1  | MonPro(8, 1) = 7 |
| 0     | MonPro(7, 7) = 12 |                  |

- return $x = \text{MonPro}(12, 1) = 4$

## References

[Computer Arithmetic Fundamentals: Montgomery](http://koclab.cs.ucsb.edu/teaching/cs154/docx/Notes7-Montgomery.pdf)

[Montgomery Multiplication](https://cp-algorithms.com/algebra/montgomery_multiplication.html)
