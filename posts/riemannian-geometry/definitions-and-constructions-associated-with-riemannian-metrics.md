---
layout: post
title: Definitions and Constructions Associated with Riemannian Metrics
math: true
---

Hey everyone, welcome to my first ever entry!
In this series of posts, I'll be taking a deep dive into Riemannian geometry by working through John M. Lee's *Riemannian Manifolds - An Introduction to Curvature*.
I've always wanted to learn about this topic ever since I learned that the theory of general relativity makes use of the machinery of Riemannian geometry.
Riemannian geometry also makes its appearance in machine learning through non-convex optimization on manifolds and methods based on the natural gradient, as well as in reinforcement learning with the natural policy gradient.
However, I will not get a chance to take the relevant class at Berkeley (boo!) so I've decided to take matters into my own hands.

The way this and other posts will be structured is that I'll be writing down the most salient points, as well as proofs that I've attempted on my own.
If you find any errors, please let me know!
With that, let's get right to it!

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

\[
  g_p = F_{ij}\mathrm{d}x^i \otimes \mathrm{d}x^j,
\]

where $(F_{ij})$ is a positive-definite matrix.
With this choice, $g_p$ is symmetric and positive-definite.

Now, observe that since the $\left\\{U_p\right\\}$ form an open cover of $M$, we can find a partition of unity $\left\\{\psi_p\right\\}$ subordinate to the cover.
Since the support of any $\psi_p$ is contained in $U_p$, $\psi_pg_p$ is a smooth $2$-field on all of $M$, taking $g_p$ to be zero outside $U_p$.
Then, define $g$ as

\[
  g = \sum_{p \in M}{\psi_pg_p}.
\]

This is a well-defined sum throughout the manifold as the set of supports is locally finite.
Furthermore, $g$ is positive-definite and symmetric since every $g_p$ has the same property.

Thus, $g$ is a Riemannian metric, and $(M, g)$ is a Riemannian manifold.

\[
  \tag*{$\blacksquare$}
\]

If we have two Riemannian manifolds $(M, g), (\tilde{M}, \tilde{g})$, as well as a diffeomorphism $\phi: M \to \tilde{M}$, then we say that $\phi$ is an *isometry* if $\phi^* \tilde{g} = g$.
Riemannian geometry is concerned with the study of properties that are preserved under these isometries.
