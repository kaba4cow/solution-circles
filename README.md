# Problem

Given:

- An array of circles `circles`, defined as `(x, y, r)`, where `x` and `y` are center coordinates and `r` is radius.
- A direction vector `dir`
- A width value `width`

Determine whether there exists an infinite strip of width `width` aligned with `dir` which does **not intersect** any of the given circles.

# Solution

## Step 1: Rotate world space

Rotate the coordinate space so that `dir` becomes aligned with horizontal axis `(1, 0)`.

- Calculate rotational angle `theta` from `dir` to `(1, 0)`
- Rotate the center of each circle by `theta`

## Step 2: Calculate circle intervals

After rotation, each circle now occupies a vertical interval from `y - r` to `y + r`.

- For each circle, calculate its vertical interval and store it as `(bottom, top) = (y - r, y + r)`
- Collect all intervals into an array `intervals`

## Step 3: Sort circle intervals

- Sort the `intervals` by their `bottom` coordinate.

## Step 4: Merge overlapping intervals

- Create an empty dynamic array `merged`
- Iterate through sorted `intervals`, merging overlapping ones (intervals `(a, b)` and `(c, d)` overlap if `b >= c`)

## Step 5: Find a valid gap

- Check for vertical gaps between adjacent intervals in `merged`
- For each pair of intervals `(a, b)` and `(c, d)` calculate the gap: `gap = c - d`
- If any calculated `gap` is greater than or equal to `width`, return `true`
- If no such `gap` exists, return `false`
