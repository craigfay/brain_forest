# Eigenvalues and Eigenvectors

[3Blue1Brown](https://www.youtube.com/watch?v=PFDu9oVAE-g): Most vectors will have their angle changed by a transformation, but eigenvectors are the vectors whose angles are preserved after a [[Matrix (Linear Algebra)|transformation]]. The eigenvalue is just a scalar that describes the stretching / squishing effect on an eigenvector.

- Eigenvalues will be negative in the event that an eigenvector’s direction is reversed.
- Eigenvectors can intuitively be visualized as the transformation’s axis of rotation.
- We can find eigenvalues and eigenvectors by solving for v and 𝛌 in the equation Tv = 𝛌v, visualizing 𝛌 as a matrix full of zero, except for 𝛌s down the main diagonal.

The condition for 𝜆 to be an eigenvalue of T is det (T - 𝜆I) = 0.
