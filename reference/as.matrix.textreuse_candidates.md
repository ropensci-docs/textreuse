# Convert candidates data frames to other formats

These functions convert a `textreuse_candidates` object to dense or
sparse matrices.

## Usage

``` r
# S3 method for class 'textreuse_candidates'
as.matrix(x, ...)

as_sparse_matrix(x)
```

## Arguments

- x:

  An object of class
  [`textreuse_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_compare.md).

- ...:

  Additional arguments.

## Value

A similarity matrix with row and column names containing document IDs.
