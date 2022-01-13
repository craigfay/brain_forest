According to [[Norman J Wildberger]].
https://www.youtube.com/watch?v=XoTeTHSQSMU

## Field Theory
We think of a field as an arena on which to do arithmetic. We must distinguish between **finite** and **unbounded** fields.

A few key features of field theory:
- There are two **binary operations**: Addition and Multiplication.
- There is also one **unary operation**: This is the operation of taking multiplicative inverses.
	- If a != 0, then a * inv(a) = 1
- There are some special elements: 0, 1, and -1.
	- 0 + a = a
	- 0 * a = 0
	- 1 + a = a
	- 1 + -1 = 0
- There are some laws that are satisfied: commutativity, associativity, and distributivity.

Wildberger introduces tables for each of the binary operations that we use to lookup answers to addition and multiplication questions. *Is there an algorithm that we can use so that we don't need tables?* 


We'll use a feature characteristic of [[Modular Arithmetic]], and have values wrap around to the other side of our scalar field when they would otherwise exceed the limits of the field.

In the finite field F7 = { -3, -2, -1, 0, 1, 2, 3 } for example,
4 + 4 = 8 % 7 = 1. Similarly 2 * 3 = 6 % 7 = -1.

Every element of the set has a Multiplicative inverse except 0.

Consequences:
- 0, 1, and -1 are unique. No other numbers have their properties.
- -a = -1 * a
- a - b = a + -b (subtraction is defined)
- a / b = a * inv(b) (division is defined) if b != 0

## Instructions for Building
1) Start with a field F. We can use an unbounded field if we insist, but it needs a different treatment.
2) Choose a geometry. There are three nice choices: One is Euclidean, and the other two are Relativistic ([[Chromogeometry]]).
3) Construct a quadratic inverse algebra: Either Cr(F), Cg(F), or Cb(F). These stand for red, green, and blue, and blue is the Euclidean flavor. This involves using the [[Linear Algebra]] of 2x2 matrices over the field F. Wildberger suggests that earlier mathmaticians struggled to understand the role of the complex numbers because an unfamiliarity with linear algebra.

### Blue
We're looking at 2x2 matrices of the form:
[a, b; -b, a] = a[1, 0; 0, 1] * b[0, 1; -1, 0]

### Red (Relativistic)
We're looking at 2x2 matrices of the form:
[a, b; b, a] = a[1, 0; 0, 1] * b[0, 1; 1, 0]

### Green (Relativistic)
We're looking at 2x2 matrices of the form:
[a + b, 0; 0, a + b] = a[1, 0; 0, 1] * b[1, 0; 0, -1]

Each one of these is a 2 dimensional subalgebra of the 2x2 matrices. This means that each one of them is closed under addition, scalar multiplication, (scalar refers to elements in the field), and multiplication. If you do any of these operations on a matrix of this form, you will produce another matrix of this form. They are also all commutative! Usually when we use matrices, we have to deal with the complexity of having multiplication that is non-commutative. Now we have a 2-dimensional version of F that is still commutative.

The original elements are preserved in this system as the diagonal entries of each matrix.

### Conjugation
The conjugate of any dihedron:
[a, b; c, d] is [d, -b; -c, a].

Importantly, conjugation commutes:
conj(r) * r = r * conj(r)

The properties of the conjugate makes the dihedral complex numbers D a "star-algebra"

Condensed Dihedron formulation:
```
d = t + xi + yj + zk

i^2 = -1
j^2 = k^2 = 1

ij =  k, jk = -i, ki =  j
ji = -k, kj =  i, ik = -j

Md = [
	 t + z, x +  y;
    -x + y, t + -z
]
```

## Quaternions
O. Rodriguez and WR Hamilton (1840s)

Motivation: Study rotations in 3D (complex are used for 2D rotations), simplify Maxwell's equation.

Dot and Cross products: Lagrange discovered studying the geometry of tetrahedrons (1770s), H Grassman. JW Gibbs, O Heaviside elevated these two operations, in part because they allow us to think about 3D rotations without a 4D structure.

Quaterions can be thought of as 4 parts, 1 scalar t, 1 3D vector [x,y,z].

Quaternion multiplication captures the vector product and dot product at the same time. A similar thing happens with dihedrons, but it is much less studied.

Multiplication of two dihedrons `(t1 + v1)` and `(t2, v2)`:

```
(t1 + v1)(t2, v2) = t + v where
t = (t1)(t2) - dot(v1, v2)
v = (t1)(v2) + (t2)(v1) + cross(v1, v2)
```

The dot product here is not the usual one. It is relativistic! The same kind of geometry that occurs in special relativity.

```
// The 2nd and 3rd entries are inversed when
// compared to the euclidean dot product formula
dot(v1, v2) = (x1)(x2) - (y1)(y2) - (z1)(z2)

// The 1st row is inversed when compared
// to the euclidean cross product formula
cross([x1, y1, z1], [x2, y2, z2]) = [
  -(y1)(z2) +  (z1)(y2);
   (z1)(x2) + -(x1)(z2);
   (x1)(y2) + -(y1)(x2);
]
```

NJ Wildberger's PhD student Genadiy Wado Wadigdo wrote a thesis on this story. It's all about the general theory of dot and cross products in 3D space.

We can represent [[Quaternions]] as a 2x2 matrix of Dihedral complex numbers. 