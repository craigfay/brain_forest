# Euclid's Elements
(As taught by [[Norman J Wildberger]])

Written by Euclid in 300 B.C. in [[Ancient Greece|Greece]].

## Introduction: Definitions
Euclid introduces (how many?) definitions, most notably:
* A **point** is that which has no part.
* A **line** is that which has no length.
* The **extremeties** of a line are points.
* **Parallel lines** are those which do not meet if extended.

## Introduction: Axioms
Taken by Euclid to be self evident

1) Things which are equal to the same thing are also equal to one another.
2) The whole is greater than the part. 

## Introduction: Postulates
These are assumptions that Euclid lays as a foundation for his remaining constructions.

1) If you have any two points, you can always draw a line between them.
2) If you have a line, you are always allowed to extend it arbitrarily in either direction.
3) If you have two points, you can always draw a circle whose center is at one point, and whose edge intersects the second point.
4) Any two right angles are the same.
5) If you have a line, and a point not on the line, then there is exactly one line that is parallel to the line that runs through the point. This is called the **parallel postulate**, and famously acts as a gateway to non-Euclidean geometries.

## Book 1 - Proposition 1: Constructing Equilateral Triangles
Given two points, Euclid shows how to build an equilateral trangle using the intersection of two circles with centers and edges passing through the two points.

Euclid cheats a little, because he doesn't provide a postulate guaranteeing that these two circles actually meet. It appears obvious visually that they meet, but it isn't a logical consequence of the postulates.

![Pythagorean Theorem](media/equilateral_triangle_construction.webp)

## Book 1 - Proposition 47, 48: Pythagorean Theorem
Euclid visuallized the pythagorean theorem as the sum of the areas of three squares.
He called them Q1, Q2, and Q3, because the ancient Greeks used to like the word "quadrature". Propsition 48 is concerned with the inverse: If areas of such configured squares matches this description, the angle formed by Q1 and Q2 is a right angle.

![Pythagorean Theorem Construction](media/pythagorean_theorem.webp)

## Book 2 - Proposition 4
Euclid offers a visual geometric proof of the equation:
(a + b)^2 = a^2 + b^2 + 2ab

![**(a + b)^2 = a^2 + b^2 + 2ab**](media/euclids_elements_book_2_prop_4.webp)

## Book 2 - Proposition 14
Euclid shows how to solve quadratic equations geometrically.
We look for an *x* such that x^2 = ab. We can solve this by constructing a circle starting from B and taking the length of the vertical line joining B and F.

![Book 2 Proposition 14](media/euclids_elements_book_2_prop_14.webp)

## Book 3: Circles
Euclid displays theorems about circles, including:
* Angles subtended by chords of a circle
* Horned angles formed by lines tangent to a circle

## Book 4: Inscribed Polygons

## Book 5: Proportions
This book is particularly interesting for foundational issues related to **Irrational Numbers**. The greeks thought of **magnitude** as a fundamental object of interest. Magnitude was similar to the modern idea of a **number**, but without a unit. They would have said that lines, areas, and angles all have magnitude.  Instead of algebraicly, they were thinking geometrically.

They believed that some operations were always possible:
* Check which of two magnitudes was greater.
* Form whole-number multiples of any magnitude.

They believed that the proportions between magnitudes were more important than the magnitudes themselves.

## Book 5: Commensurability
The greeks thought of two magnitudes as **commensurable** if they were both multiples of a third magnitude. As modern people, we would instead say that these two magnitudes have a **common factor**.

Because the third magnitue in this definition could be arbitrarily small, the greeks thought that all magnitudes were commensurable, and they were quite shocked to discover otherwise.

The pythagoreans had a theory about how proportions could explain many aspects of the world, most notably, cosmic motion and the theory of music. We now have formal names for [[Musical Interval|intervals between two tones]] whose frequencies form particular ratios:

* 2:1 - Octave
* 3:2 - Fifth
* 4:3 - Fourth
* 16:9 - Minor Seventh (a composition of two perfect fourths)

The greeks were famously confounded by the following discovery: Given any square, the length of its side and the length of its diagonal are not commensurable. This leads to the theory of [[Irrational Numbers]]. Today, we would say that this ratio is proportional to the square root of 2, but the greeks didn't have a way of conceptualizing roots.

This irrationality also arises from studying the [[Circle of Fifths]]. By repeatedly traveling upwards by perfect fifths, you should arrive back to a multiple of your original tone after twelve steps. This corresponds to the fact that you can take (3/2)^12 to produce 129.7. This value is frustratingly close to 2^7 = 128. This fact is the source of much subtle difficulty in the theory of music in preceding millenia.

Dealing with proportions that are commensurable is relatively easy. We can express equalities and inequalities between two proportions in the following ways:
* a:b = c:d <=> a\*d = b\*c
* a:b < c:d <=> a\*d < b\*c
* a:b > c:d <=> a\*d > b\*c

Unfortunately, this type of arithmetic only works for commensurate proportions. The question that Euclid had to surmount the problem of comparing two proportions that weren't necessarily commensurate. This problem was solved by [[Eudoxus]], and described here in Book 5 by Euclid.

## Book 6: Similar Figures
* Rules for identifying similar triangles

## Book 7,8,9: Number Theory
Not directly related to geometry.

## Book 10: Incommensurable Numbers
- How to deal with nested radicals.

## Book 11,12,13: Solid Geometry (3D)
- A **solid** is that which has length, breadth, and depth.
- An extremity of a solid is a **surface**.
- A straight line is at right angles to a plane when it makes right angles with all line in the plane that meets it.

These later books represent Euclid biting off more than he can chew; 3D geometry is difficult, and Euclid makes a number of mistakes and logical inconsistencies.

Proposition 2 of Book 12 states: Circles are to each other as squares on the diameters. We would say that the area of a circle is proportional to the square of it's radius. Euclid knew that this should be demonstrated, and employed [[Eudoxus|Eudoxus' theory of exhaustion]].

## The 5 Platonic Solids
This part of the text culminates in a description of the 5 platonic solids:
- Tetrahedron
- Cube
- Octahedron
- Icosahedron
- Dodecahedron

## Interpretation
Despite its shortcomings, *Elements* was substantial enough to form a groundwork for the next 2000 years of mathematics.

