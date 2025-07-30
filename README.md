# Problem

Given:

- An array of circles `circles`, each with center `(x, y)` and a `radius`
- A direction vector `dir = (dx, dy)`
- A width value `width`

Determine whether there exists an infinite line of width `width` aligned with `dir` which does not intersect any of the circles in `circles`.

# Solution

## Rotate world space

Rotate the coordinate space so that `dir` becomes aligned with horizontal axis `(1, 0)`.

1. Calculate angle `angle` of `dir`
2. Rotate `(x, y)` of each circle in `circles` by `angle`, store as `(x', y')`
