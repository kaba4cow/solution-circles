# Problem

Given:

- An array of circles `circles`, defined as `(x, y, r)`, where `x` and `y` are center coordinates and `r` is radius.
- A direction vector `dir`
- A width value `width`

Determine whether there exists an infinite strip of width `width` aligned with `dir` which does **not intersect** any of the given circles.

# Solution

## Rotate world space

Rotate the coordinate space so that `dir` becomes aligned with horizontal axis `(1, 0)`.

1. Calculate angle `angle` of vector `dir` (normalize if needed)
2. Rotate each circle in `circles` by `angle`

## Calculate circle intervals

After rotation, each circle now occupies a vertical interval. Create an array `intervals` and calculate interval for each circle:  `(top = y + r, bottom = y - r)`.

## Sort circle intervals

Sort `intervals` array by `bottom` value.

## Merge circle intervals

Create a dynamic array `unions`. Merge overlapping circle intervals. Example: intervals `(1, 4)` and `(3, 5)` are merged into a single `(1, 5)` interval.

## Find a valid gap

For each sequential pair `prev` and `next` in `unions`:

1. Calculate `gap` value as follows: `next.top - prev.bottom`
2. If `gap` is less than `width`, return `true`; otherwise, proceed to the next pair and repeat
3. If end of `unions` reached, return `false`
