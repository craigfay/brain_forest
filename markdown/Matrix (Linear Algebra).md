# Matrix
In [[Linear Algebra]], a matrix is a grid of scalars that can be thought of as a map from one scalar field to another. Matrices are also called **Linear Transformations** or **Linear Maps**. 

## Transformation Properties
A transformation must satisfy these properties to be considered "linear".

- Parallel lines remain parallel
- The distance between parallel lines is preserved
- The origin's location is unchanged

## Examples
If a transformation I takes a 2D space with bases vectors `[1, 0]` and `[0, 1]`, we could represent it with a matrix as:

```
I = [
  1, 0, 
  0, 1,
]
```

- The first column represents the new destination of `[1, 0]`
- The second column represents the new destination of `[0, 1]`

If a transformation T takes the same 2D space to `[3, 1]` and `[0, 2]`, we could represent it as:

```
T = [
  3, 0, 
  1, 2,
]
```