
## 14.1 Differentiation on a Manifold?

For each linear transformation that acts on a space, there is some structure that is preserved.
- The **orthogonal group** preserves the **metric** structure. 
- The **unitary group** preserves the **Hermitian** structure.
- The **symplectic group** preserves the **(???)** structure.

A vector space is a very specific type of space. We need something more general for modern physics.

Even Euclidean space is not a vector space, because vector space needs an origin. Euclidean space is an example of an [[Affine Space]]. An affine space is like a Euclidean Space that "forgets" the origin, and has a consistent notion of a parellelogram. Specifying a point as the origin allows vector addition to be defined using the **parellelogram law** (§13.3).

Einstein's curved spacetime is more general than a vector space. It is a 4-manifold, but does require some additional local structure. Such a structure could provide:
- A measure of distance between points.
- The area of a surface.
- The angle between curves. *What does that mean?*

These are all vector space notions. The vector space in question is the $n$-dimensional **tangent space** $T_p$ of a typical point $p$ on the manifold $M$. We should think of $T_p$ as the immediate vicinity of $p$, infinitely stretched out; The higher dimensional analog of a line tangent to a curve (see fig 12.6).

The group structures from Chapter 13 can have local relevance at the individual points of a manifold. Einstein's spacetime has a local structure given by a **Lorentzian Pseudo-Metric** in each tangent space, whereas the phase spaces (§12.1) of classical mechanics have local **symplectic** structures.

Can we apply calculus on manifolds? There is no general notion of differentiation within $M$. We could do calculus on a particular coordinatized patch of $M$ by using partial derivative operators, but our answers wouldn't be compatible between patches.

The **exterior derivative** of §12.6 actually does apply to general, smooth, unstructured manifolds, *and* it agrees between patches, but it applies only to $p$-forms, and does not yield information about how the $p$-form is varying.

A complete notion of the *derivative* of a quantity (like a vector or tensor field) on our general smooth manifold would have to be coordinate independent. **It would enable us to express how a vector or tensor field varies as we move from place to place.**

## 14.2 Parallel Transport

*Imagine taking the curve of a function in 2D and wrapping a graph of it around a curved surface. How. would you measure rise-over-run, now that the direction of the X and Y axis are no longer clear at any point?*

To measure rate-of-change, we need a **constant** field on $M$. (Remember §10.3) A smooth manifold does not necessarily have **parallelism**. The coordinate systems on two overlapping patches are not guaranteed to have parallel basis vectors.

We can use **parallel transport** to (???).

We can parallel transport by embedding our manifold (say for example the sphere, $S_2$) into a larger ambient space, (say $E_3$). As we transport the tail of a tangent vector $v$ around the surface of the sphere, the rest of its body will point off into the ambient space. We need our notion of parallelism to only include tangent vectors. *This is intuitive, but why?* We project the transported vector back onto tangency with the sphere. *How do we decide on a projection scheme?*

The new notion of parallelism that this leads us to has a property called **path dependence**. The type of parallel transport here will can change the rotation of the tangent vectors, but not their magnitude. (Other types of parallel transport can change magnitude.) 

## 14.3 Covariant Derivative
How can we use parallel transport to define a derivative operator on a curved surface?

We get the  covariant derivative by comparing a vector field with vectors produced by parallel transport. The covariant derivative is also called a **connection**.

We subtract the parallel transported vector from the vector field?