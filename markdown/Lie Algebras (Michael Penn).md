# Lie Algebras (Michael Penn)
https://www.youtube.com/watch?v=Sxy4WDIUs6M


An **[[algebra]]** starts with a **vector space** (over a field). This includes both vectors (which are tuples of scalars) and scalars. The algebra is defined when it endows the vector space with a **multiplication**.

The vector space is taken to already have scalar-vector multiplication, and vector-vector addition.

We typically consider a vector space over the complex numbers, because they are the simplest field that is algebraically closed.

Multiplication is denoted $*$. It takes 2 inputs from $A$, and yields one output, also from $A$. You can think of it as a **bi-linear map**. Left multiplication by any element and right multiplication by any element should be a linear transformation in the vector space. 

Assume that $\alpha$,  $\beta$, and $\gamma$ are all vectors.
Assume that $\mathbb{C}_{1}$, $\mathbb{C}_{2}$, $\mathbb{C}_{3}$, are all scalars.

We want multiplication to satisfy a few properties:
- $\mathbb{C}_{1} (\alpha * \beta) = (\mathbb{C}_{1} \alpha) * \beta = \alpha * (\mathbb{C}_{1} \beta)$
- $\alpha * (\beta + \gamma) = \alpha * \beta + \alpha * \gamma$ (left-side distributivity)
- And right-side distributivity?

Notice that associativity and commutativity are missing. They aren't required for the strictest definition of an algebra.

## Simple Example: $\mathbb{C}$
Consider $A = \mathbb{C}$. We can do this because any field is a vector space over itself. $*$ in this case is just complex number multiplication. This gives us associativity, commutativity, and lots of inverses. Everything is invertable except for $0$.

## Another Example: $\mathbb{C}[x]$
The classic example of a commutative and associative algebra is the polynomials with complex coefficients, $\mathbb{C}[x]$. We might call this the **"polynomial algebra"**, or perhaps a **"polynomial ring"**. It doesn't have any inverses.

If we tried to take inverses, we'd probably try to expand it as a power series, but then it's no longer a finite linear combination of things. (No longer a polynomial)

You would probably learn about this in an [[Abstract Algebra]] class. At the end of the first semester, you might be shown $k[x]$, where $k$ is an arbitrary field. It has interesting properties like **unique factorization**.

