## 13.7 Tensor Representation Spaces; Reducability
Comprehension: 2/5

A **representation space** is a vector space that a family of linear transformations (representing a group) will act on.

Given a group $G$ and its representation space $V$, its *dual space* $V^{*}$ is also a suitable representation space.

A **reducible representation** is one that has a choice of basis for which all the matrices of the representation can be put in the form:

$$
\begin{pmatrix}
A & C \\ O & B
\end{pmatrix}
$$
Where $A = p \times p$, $B = q \times q$, $C = p \times q$, with $p, q \geq 1$ for fixed $p$ and $q$.

If the representing matrices all have this form, then the $A$ matrices and $B$ matrices each individually constitute a smaller representation of $G$.

If the $C$ matrices are all zero, we get the case where the representation is the direct sum of the two smaller representations.

A representation is call **irreducible** if it is not reducible (with $C$ present or not).

A representation is called **completely reducible** if we never get the above situation (with non-zero $C$), so that it is a direct sum of irreducible representations.

**Semi-Simple Groups** are a well studied type of group. **Compact** simple groups have only representations that are completely reducible. See §12.6, Fig. 12.13 for a definition of "compact".

It it sufficient to study *irreducible* representations of such a group, every representation being just a direct sum of these irreducible ones. In fact, every irreducible representation of a compact semi-simple group is finite-dimensional.

What is a **semi-simple group?** There is a structure called the **Killing 
form** $K$, constructed from the *structure constants* of §13.6. A group is semi-simple if $K_{\alpha\beta}$ is *non-singular*.

**Real Forms**: Given a structure constant ${\gamma_{\alpha\beta}}^{\chi}$, a real form is the compact real number Lie algebra obtained when $-K_{\beta\alpha}$ is positive-definite? *Not quite, but close*...

*Any complex semi-simple Lie group has exactly one **real form** (definition needed) which is compact!*


## 13.8 Orthogonal Groups

We saw in the beginning of §13.3 how to represent O(3) and SO(3) as matrices. These groups represent symmetries of the sphere given by $x^{2} + y^{2} + z^{2} = 1$.

We can use index notation to describe an $n$ dimensional sphere as $g_{ab}x^{a}x^{b} = 1$, which stands for ($x^{1})^{2} + ... + x^{n})^{2}$, the components $g_{ab}$ being given by:

$$
g_{ab} =
	\bigg\{
		\begin{array}{lr}
		 1 \text{ if } a = b \\
		 0 \text{ if } a \ne b \\
		\end{array}
$$

*Here we should imagine that the effect of transformations is not to distort space, but to adjust the bases that we use to measure them!*

The **orthogonal group** is the group of linear transformations in $n$ dimensions that preserve a given positive-definite $g$. Preserving $g$ means that an orthogonal transformation has to satisfy:

$$
{g_{ab}} {{T^{a}}_{c}} {{T^{b}}_{d}} = g_{cd}
$$
This is an example of the **active tensor rule** from §13.7, as applied to $g_{ab}$. Another way of saying this is that the metric form $ds^{2}$ is unchanged by orthogonal transformations.

The real orthogonal $n \times n$ matrices provide a concrete realization of the group $O(n)$. To specialize to the non-reflective $SO(n)$, we require that the determinant of the matrices be equal to unity.

### Pseudo Orthogonal Groups

We can also consider the corresponding **pseudo-orthogonal** groups $O(p, q)$ and $SO(p, q)$ that are obtained when $g$, though [[Non-Singular (Matrix)|non-singular]], is not necessarily [[Positive Definite (Matrix)|positive definite]].

How different are all the combinations of $O(p, q)$ in any dimension $n$? 
- They all have the same dimension, $\frac{1}{2}n(n - 1)$ 
- They are all [[Real Forms]] of the same complex group $O(n, \mathbb{C})$, which is the complexification of $O(n)$.  
- Physicists often treat the combinations interchangeably, which Penrose suggests is inappropriate, even though there are great insights to be found in ignoring the distinctions.
- They are distinguished by a certain set of inequalities on the matrix elements, such as $\det T = 0$.
- These inequalities are often violated in physics. For example, complex numbers can have real significance in quantum mechanics.
- This idea is related to the "can of worms" alluded to in §11.2.


### Lorentz Group
The case when $p = 1$ and $q = 3$ (or $p=3$ and $q = 1$) is called the [[Lorentz Group]].
- It has the same symmetries as the hyperbolic 3 space of §2.7 and as the [[Riemann Sphere]], as achieved by the Mobius transformations of §8.2. 
- It is critically important in [[Twistor Theory]] as described in §33.2.

### Comparing Real and Complex Groups

In complex group representations, the notion of **signature** disappears, because there are linear transformations that can convert a $-1$ into a $1$ on the diagonal of $g_{ab}$ and vice-versa. The only **invariant** of $g$ is its **rank**, which which is the number of non-zero terms in its diagonal realization. For. [[Non-Singular (Matrix)|non-singular]], matrices the rank has to be $n$.

## 13.9 Unitary Groups

The group $O(n, \mathbb{C})$ represents one way to generalize a rotation group from the real to the complex numbers. Unitary groups are another way to do the same.

The orthogonal group is concerned with preserving the **quadratic form**. The unitary group is concerned with preserving the **Hermitian form**, and uses complex linear transformations to do so.

The **complex conjugation** operation is often called **Hermitian conjugation**. It identifies the complex-conjugate space with the dual space, and is centrally important to quantum mechanics and Twistor theory. It is often represented with the dagger symbol or an asterisk.

The group of unitary tranformations in n dimensions is called the *unitary group* $U(n)$. We get the psuedo-unitary group $U(p,q)$ when the hermitian conjugate operator has the form $(p,q)$.

If the tranformations have a determinant of 1, then we obtain $SU(n)$ and $SU(p, q)$!

## 13.10 Symplectic Groups

Often denoted $Sp(2n, F)$ where $F$ is a field.

Orthogonal and Unitary groups are considered **classical** groups. **Symplectic** complete the list of classical groups. They are useful for representing classical (§20.4) and quantum (§26.3) physics.

*What is bilinear form?*
It looks like this? $g(x,y) = g(y,x)$

The symplectic group is like the orthogonal group, except with an antisymmetry property and linearity.

An anti-symmetric $n \times n$ matrix $S$ can only be non-singular if $n$ is even.