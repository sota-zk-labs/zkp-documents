# Structured Reference String (SRS)

Let $e$ be a [bilinear map pairing](pairings_or_bilinear_map.md) groups $G, G_t$ of prime order $p$. Assume $g \in G$ is a generator,
and $D$ sets an upper bound on the polynomials degrees which we would like to support commitments to.

The structured reference string (**SRS**) consists of encodings in $G$ of all powers of a random nonzero field element $\tau \in F_p$.
Here, $\tau$ is an integer randomly selected from the range $\{1, . . . , p−1\}$. The elements constituting the **SRS**
are $(g, g^{\tau} , g^{\tau^2} , ... , g^{\tau^D})$.

It is noteworthy that the value $\tau$ is toxic waste that must be discarded because it can be used to destroy binding and break the
integrity of commitments.
