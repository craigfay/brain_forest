# Road to Reality
An summary of *Road to Reality* by [[Roger Penrose]].

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

*Here we should imagine that the effect of transformations is not to distort space, but just the bases that we use to measure them!*

