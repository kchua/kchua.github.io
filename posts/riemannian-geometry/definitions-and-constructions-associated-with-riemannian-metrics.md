---
layout: post
title: Definitions and Constructions Associated with Riemannian Metrics
math: true
---

Hey everyone, welcome to my first ever entry!
In this series of posts, I'll be taking a deep dive into Riemannian geometry by working through John M. Lee's *Riemannian Manifolds - An Introduction to Curvature*.

I've always wanted to learn about this topic ever since I found out that general relativity makes use of the tools developed in this area.
Riemannian geometry also makes its appearance in machine learning through non-convex optimization on manifolds and methods based on the natural gradient, as well as in reinforcement learning with the natural policy gradient.
However, I will not get a chance to take the relevant class at Berkeley (boo!) so I've decided to learn it myself!

For these notes, I'll be writing down the most salient points, as well as proofs that I've attempted on my own.
If you find any errors, please let me know.
With that, let's get started!

## Definitions

We begin by defining the additional structure on a general smooth manifold that we will be concerned with throughout our study of Riemannian manifolds.

**Definition.** A *Riemannian metric* on a smooth manifold $M$ is a smooth (covariant) $2$-tensor field $g \in \mathcal{T}^2(M)$ that is symmetric and positive-definite.

We refer to $(M, g)$ as a *Riemannian manifold*.
Observe that the Riemannian metric defines an inner product on every tangent space of the manifold.
Having this notion of an inner product allows us to define familiar concepts such as norms and angles for each tangent space.

One may ask if Riemannian metrics even exist (of course, beyond the natural Riemannian metric on Euclidean space).
The following proposition demonstrates that in fact, *every* smooth manifold can be endowed with a Riemannian metric.

**Proposition.** *Every smooth manifold $M$ admits a Riemannian structure*.

*Proof.* For every $p \in M$, find a coordinate chart $(U_p, \phi_p)$ containing $p$.
Then, we can locally define a smooth $2$-tensor field $g_p \in \mathcal{T}^2(U_p)$ by defining

<div class="disp-math">
\[
  g_p = F_{ij}\mathrm{d}x^i \otimes \mathrm{d}x^j,
\]
</div>

where $(F_{ij})$ is a positive-definite matrix.
With this choice, $g_p$ is symmetric and positive-definite.

Now, observe that since the $\left\\{U_p\right\\}$ form an open cover of $M$, we can find a partition of unity $\left\\{\psi_p\right\\}$ subordinate to the cover.
Since the support of any $\psi_p$ is contained in $U_p$, $\psi_pg_p$ is a smooth $2$-field on all of $M$, taking $g_p$ to be zero outside $U_p$.
Then, define $g$ as

<div class="disp-math">
\[
  g = \sum_{p \in M}{\psi_pg_p}.
\]
</div>

This is a well-defined sum throughout the manifold as the set of supports is locally finite.
Furthermore, $g$ is symmetric since every $g_p$ has the same property, and $g$ is positive-definite since every $g_p$ is positive definite and every $p \in M$ is contained in one of the supports.

Thus, $g$ is a Riemannian metric, and $(M, g)$ is a Riemannian manifold.

<div class="disp-math">
\[
  \tag*{$\blacksquare$}
\]
</div>

If we have two Riemannian manifolds $(M, g), (\tilde{M}, \tilde{g})$, as well as a diffeomorphism $\phi: M \to \tilde{M}$, then we say that $\phi$ is an *isometry* if $\phi^* \tilde{g} = g$.
Riemannian geometry is concerned with the study of properties that are preserved under these isometries.

Observe that as a consequence of the symmetry of the metric, we have that in local coordinates,

<div class="disp-math">
\[
  g = g_{ij}\mathrm{d}x^i \mathrm{d}x^j
\]
</div>

### Derived Metrics

Now that we've defined what a Riemannian metric, let's look at how we can derive new metrics from metrics on other spaces.

#### Induced Metric

Consider a Riemannian manifold $(M, g)$ and an immersed submanifold $N \subseteq M$.
Then, we can define the *induced metric* $\tilde{g}$ on $N$ as the pullback of $g$ under the inclusion $i: N \to M$, i.e. $\tilde{g} = i^* g$.
Using the identification of the tangent vectors of $N$ with the tangent vectors on $M$ that are also tangent to $N$, we see that the induced metric is essentially $g$ restricted to the subspace of vectors that are tangent to $N$.

#### Metrics on Product Manifolds

If $(M_1, g_1), (M_2, g_2)$ are Riemannian manifolds, then on the product manifold $M_1 \times M_2$, we can obtain the natural identification of tangent spaces $T_{(p, q)}(M_1 \times M_2) \cong T_pM_1 \oplus T_qM_2$.
Consequently, we can define a natural metric $g$ on the product as

<div class="disp-math">
\[
  g(X_1 + X_2, Y_1 + Y_2) = g_1(X_1, Y_1) + g_2(X_2, Y_2),
\]
</div>

where $X_1, Y_1 \in T_pM_1$ and $X_2, Y_2 \in T_qM_2$.

#### Covering Metrics

Supposed that $M, N$ are smooth manifolds, and assume that there exists a smooth covering map $\pi: M \to N$.
Remember that a *deck transformation* (on a smooth covering space) is a diffeomorphism $\phi: M \to M$ such that $\pi \circ \phi = \pi$.
Then, given a Riemannian metric $g$ on $N$, we can pull back the tensor field onto $M$ and obtain a Riemannian metric $\tilde{g} = \pi^* g$.
The metric $\tilde{g}$ is often referred to as a *covering metric*, and $\pi$ is then a *Riemannian covering*.

**Proposition.** *The covering metric is invariant under deck transformations.*

*Proof.* Using properties of pullbacks, we have that for any deck transformation $\phi: M \to M$,

<div class="disp-math">
\[
  \tilde{g} = \pi^* g = (\pi \circ \phi)^* g = \phi^* \pi^* g = \phi^* \tilde{g},
\]
</div>

proving the desired claim.

<div class="disp-math">
\[
  \tag*{$\blacksquare$}
\]
</div>

The proposition above has the following natural converse.

**Proposition.** *Assume that $(M, g)$ is a Riemannian manifold and $N$ a smooth manifold such that $\pi: M \to N$ is a smooth normal covering map.
Then, if $g$ is invariant under all deck transformations, then $g$ descends to a Riemannian metric $\tilde{g}$ on $N$.*

*Proof.* Let $p \in N$.
Since $N$ is evenly covered, there exists an open neighborhood $U_p \subseteq N$ of $p$ such that every component of $\pi^{-1}(U_p)$ is diffeomorphic to $U_p$ through $\pi$.
Choosing one of these components $V$ amounts to a choice of section $\pi^{-1}_V$ of $\pi$.
Define the Riemannian metric locally to be $\tilde{g} = \left(\pi^{-1}_V\right)^* g$.
To see that this is well-defined, consider another component $V'$.
Then, since the cover is normal, there exists a deck transformation $\rho$ taking $V$ to $V'$.
Since $g$ is invariant under all deck transformations,

<div class="disp-math">
\[
  \left(\pi_{V'}^{-1}\right)^* g = \left(\rho \circ \pi_V^{-1}\right)^* g = \left(\pi_V^{-1}\right)^* \rho^* g = \left(\pi_V^{-1}\right)^* g.
\]
</div>

Thus, we have a well-defined Riemannian metric on an open neighborhood of every point.
These local metrics agree on overlaps, and thus by the gluing lemma, we obtain a global Riemannian metric $\tilde{g}$ on all of $N$.

<div class="disp-math">
\[
  \tag*{$\blacksquare$}
\]
</div>

## Constructions

Let's look at what we can do once we have a Riemannian metric on a smooth manifold.

### Raising and Lowering Indices (Musical Isomorphisms)

A Riemannian metric allows us to convert tangent vectors into tangent covectors and vice versa.
For any $p \in M$ and $v \in T_pM$, we can obtain a covector $v^\flat$ by defining

<div class="disp-math">
\[
  v^\flat(w) = g_p(v, w).
\]
</div>

In local coordinates, we can write this covector as

<div class="disp-math">
\[
  v^\flat = (v^\flat)_ i \mathrm{d}x^i, \quad \text{where} \quad (v^\flat)_ i = g_{ij}v^i.
\]
</div>

We have, in effect, *lowered* the index $i$, thus the name (and the flat notation).

Naturally, we can ask if an inverse operation exists.
First, observe that the action of lowering an index is linear, given by the positive-definite matrix $(g_{ij})$.
Thus, if we let $g^{ij} = (g_{ij})^{-1}_{ij}$, then for any $p \in M$ and $\omega \in T_p^* M$, we can define a tangent vector $\omega^\sharp$ as

<div class="disp-math">
\[
  \omega^\sharp = (\omega^\sharp)^i\frac{\partial}{\partial x^i}, \quad \text{where} \quad (\omega^\sharp)^i = g^{ij}\omega_j.
\]
</div>

Thus, the operation corresponds to *raising* an index, and thus the sharp notation.

To see the importance of the ${}^\sharp$ operator, recall the gradient of a function $f$ as defined in a standard multivariable calculus class, which is a tangent field defined on all of $\mathbb{R}^n$.
Although the differential $df$ of a function $f \in C^\infty(M)$ is naturally a covector field, we can extend the concept of a gradient field to an arbitrary Riemannian manifold by letting $\nabla f = df^\sharp$.

Note that the idea of lowering and raising indices can be extended to higher-order (mixed) tensors.

### Inner Products of Tensors

As defined above, the Riemannian metric gives us an inner product on each tangent space.
In fact, the Riemannian metric gives rise to an inner product on tensor bundles as well.
Given a tensor bundle $E$ on $M$, a *fiber metric* on $E$ is a smoothly-varying inner product on each fiber.

**Lemma.** *Let $g$ be a Riemannian metric on a manifold $M$. Then, there exists a unique fiber metric on each tensor bundle $T_l^kM$ with the property that if $(E_1, \dots, E_n)$ is an orthonormal basis for $T_pM$ and $(\phi_1, \dots, \phi_n)$ is the corresponding dual basis, then the set*

<div class="disp-math">
\[
  \left\{E_{i_1} \otimes \dots \otimes E_{i_k} \otimes \phi^{j_1} \otimes \dots \otimes \phi^{j_l} \middle| 1 \leq i_1, \dots, i_k, j_1, \dots, j_l \leq n\right\}
\]
</div>

*forms an orthonormal basis for $T_l^k(T_pM)$. In fact, the desired inner product can be described in local coordinates as*

<div class="disp-math">
\[
  \left\langle F, G\right\rangle = g^{i_1r_1}\cdots g^{i_kr_k}g_{j_1s_2}\cdots g_{j_ls_l}F_{i_1\dots i_k}^{j_1\dots j_l}G_{r_1\dots r_k}^{s_1\dots s_l}.
\]
</div>

*Proof.* Choose $p \in M$, and find local coordinates $(x^1, \dots, x^n)$.
Let $(\partial_1, \dots, \partial_n)$ denote the corresponding basis of tangent vectors, and let the corresponding dual basis be $(\mathrm{d}x^1, \dots, \mathrm{d}x^n)$.
Furthermore, let $T$ denote the change of basis matrix from $(\partial_1, \dots, \partial_2)$ to $(E_1, \dots, E_n)$, so that $E_i = T_i^jE_j$.
It can be easily verified that if $S = T^{-1}$, then $\phi^i = S^i_j\mathrm{d}x^j$.
Now, from the assumption, we have that

<div class="disp-math">
\[
  g_{kl}T_i^kT_j^l = \delta_{ij} \implies g_{nl}T_j^l = g_{kl}\delta_n^kT_j^l = S_n^i\delta_{ij} = S_n^j \implies T_j^m = \delta_{ml}T_j^l = g^{mn}S_n^j \implies g^{mn}S_m^iS_n^j = \delta_{ij}. \tag{$1$}
\]
</div>

Finally, observe that by the multilinearity of the tensor product,

<div class="disp-math">
\[
  E_{i_1} \otimes \dots \otimes E_{i_k} \otimes \phi^{j_1} \otimes \dots \otimes \phi^{j_l} = T_{i_1}^{s_1}\cdots T_{i_k}^{s_k}S_{r_1}^{j_1}\cdots S_{r_l}^{j_l}\left(\partial_{s_1} \otimes \dots \otimes \partial_{s_k} \otimes \mathrm{d}x^{r_1} \otimes \dots \otimes \mathrm{d}x^{r_l}\right).
\]
</div>

It follows that the inner product simply decomposes as the product of the individual inner products.
This is a well-defined operation, because the operation is completely determined by its values on the given basis above, which is invariant under the choice of local coordinates.

<div class="disp-math">
\[
  \tag*{$\blacksquare$}
\]
</div>

After reading through that proof, I hope you appreciate this meme as much as I do!

<center>  
  <div class="center-image">
    <img src="/images/index-meme.jpg" style="display: block; width: 100%; margin: auto;"/>
  </div>
  That was a <em>lot</em> of index manipulations.<br>
  (Source: Mathematical Mathematics Memes)
</center>

*To be continued! (Last update: 01/04/2019)*
