# Complex Numbers

An augmentation to the real number system that adds a value $i = \sqrt{-1}$ to the set of all numbers.

It looks like a 2 dimensional vector space over the real numbers, but isn't. The laws of addition work the same as for vectors, but complex numbers be multiplied, which has the effect of rotation on the complex plane.  The product of two complex numbers is given by:
$$
(a + i \cdot b) \cdot (c + i \cdot d) \\
= (a \cdot c - b \cdot d) + i(a \cdot d + b \cdot c)
$$
*What makes this multiplication possible?*

Because of their differences with a vector space, we say that complex numbers are a field, much like the real numbers. **This doesn't sound right. In what way are the complex numbers a field? It feels like they should be a "domain".**

## Usefulness in Signal Processing
Take a real number $\alpha$. If you multiply it by $i$ and use it in the a exponential function, $e^{i \cdot \alpha}$ , the output (when visualized on the complex plane) always lies on the unit circle. Increasing $\alpha$ and inspecting only the real or imaginary part of such a number will yield trigonometric oscillations!
$$
e^{i \cdot \alpha} = cos(\alpha) + i \cdot sin(\alpha)
$$
The product of two of these complex exponentials satisfies this curious relationship:
$$
e^{i \cdot \alpha} + e^{i \cdot \beta} = e^{i(\alpha + \beta)}
$$
[[Roger Penrose]] calls this the "multiplication is addition" property.

**We like this property, because multiplying trig product terms is usually very messy.**

## In Quantum Mechanics
In QM, we work with so-called "wave functions", which are complex valued and denoted by $\Psi$. The [[Schrodinger Equation]] tells us what the wave function does.
 $$ i \hbar \frac{\partial}{\partial t}\Psi = \hat H \Psi $$
 Despite the centrality of $i$ in this equation, it equation can be broken up into two real equations. *This may not actually be true without sacrificing more non-locality in Quantum Mechanics. [This paper](https://arxiv.org/abs/2101.10873) claims to have proven that the real numbers are insufficient to solve equations involving certain types of entanglement.*

 