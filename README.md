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

## Determine forbidden regions

After rotation, the infinite line becomes aligned with horizontal axis `(1, 0)`, and each circle now occupies an interval `(top, bottom)` where `top = y' - radius` and `bottom = y' + radius`.

1. Map `circles` to `intervals`

Create an `intervals` array. For each circle in `circles`, map it to an interval as follows: `(x', y', radius)` -> `(top = y' - radius, bottom = y' + radius)`.

```
intervals[0] === (4, 6)
intervals[1] === (1, 3)
intervals[2] === (5, 7)
```

2. Sort `intervals` by `a` coordinate

```
intervals[0] === (1, 3)
intervals[1] === (4, 6)
intervals[2] === (5, 7)
```

3. Unite intersecting intervals

Create an `intersections` dynamic array. For intersections containing intervals in range `[n, m]`, add a new intersection to `intersections`, defined as follows: `(intervals[n].top, intervals[m].bottom)`.

```
intersections[0] === (1, 3)
intersections[1] === (4, 7)
```

Explanation:

- Interval `0` does not intersect with any other interval, so leave as is.
- Intervals `1` and `2` intersect each other so unite them as follows: `(intervals[1].top, intervals[2].bottom)`

## Find a valid gap

For each sequential pair of intersections `prev` and `next` in `intersections`:

1. Calculate `gap` value as follows: `next.bottom - prev.top`
2. If `gap` is less than `width`, return `true`; otherwise, move to the next pair and proceed with step 1
3. If end of `intersections` reached, return `false`
