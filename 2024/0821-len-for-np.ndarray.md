# 0821-len() for np.ndarray

The `len()` function in Python, when applied to a NumPy array, returns the size of the first dimension (i.e., the length of the outermost dimension). This behavior is consistent regardless of the number of dimensions the array has.

Here's how `len()` behaves for arrays with different dimensions:

* For an array with a dimension of `(3, 2)`, `len()` will return `3`. This is because the array has 3 rows, and `len()` gives the number of elements along the first axis (the number of rows in this case).
* For an array with a dimension of `(2, 3)`, `len()` will return `2`. This is because the array has 2 rows.

In summary, for a two-dimensional array defined as `shape = (m, n)`, `len(np.array)` will return `m`.
