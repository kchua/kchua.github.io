---
layout: post
title: Definitions and Constructions Associated with Riemannian Metrics
math: true
---

Hey everyone, welcome to my first post!
In this and subsequent posts, I'll be taking a deep dive into Riemannian geometry by working through John M. Lee's *Riemannian Manifolds - An Introduction to Curvature*.
The way these posts will be structured is that I'll be writing down the most salient points, as well as proofs that I've attempted on my own.
If you find any errors, please let me know!
With that, let's get right to it!

## Definitions

We begin by defining the additional structure on a general smooth manifold that we will be concerned with throughout.

**Definition.** A *Riemannian metric* on a smooth manifold $M$ is a smooth $2$-tensor field $g \in \mathcal{T}^2(M)$ that is symmetric and positive-definite.

Observe that the Riemannian metric defines an inner product on every tangent space of the manifold.
We refer to $(M, g)$ as a *Riemannian manifold*.
One may ask if Riemannian metrics even exist.
The following proposition demonstrates, in fact, that every smooth manifold can be endowed with a Riemannian metric.

**Proposition.** *A Riemannian structure can be imposed on every smooth manifold $M$*.

*Proof.* For every $p \in M$, find a coordinate chart $(U_p, \phi_p)$ containing $p$.
Then, we can locally define a smooth $2$-tensor field $g_p \in \mathcal{T}^2(U_p)$ by defining

$$g_p = F_{ij}\mathrm{d}x^i \otimes \mathrm{d}x^j,$$

where $(F_{ij})$ is a positive-definite matrix.
With this choice, $g_p$ is symmetric and positive-definite.

Now, observe that since the $\left\{U_p\right\}$ form an open cover of $M$, we can find a partition of unity $\left\{\psi_p\right\}$ subordinate to the cover.
Since the support of any $\psi_p$ is contained in $U_p$, $\psi_pg_p$ is a smooth $2$-field on all of $M$, taking $g_p$ to be zero outside $U_p$.
Then, define $g_p$ as

$$g = \sum_{p \in M}{\psi_pg_p}.$$

This is a well-defined sum throughout the manifold since the set of supports is locally finite, and furthermore, $g$ is positive-definite and symmetric since every $g_p$ has the same property.

Thus, $g$ is a Riemannian metric, and $(M, g)$ is a Riemannian manifold.
