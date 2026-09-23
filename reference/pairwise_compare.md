# Pairwise comparisons among documents in a corpus

Given a
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
containing documents of class
[`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md),
this function applies a comparison function to every pairing of
documents, and returns a matrix with the comparison scores.

## Usage

``` r
pairwise_compare(corpus, f, ..., directional = FALSE, progress = interactive())
```

## Arguments

- corpus:

  A
  [`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md).

- f:

  The function to apply to `x` and `y`.

- ...:

  Additional arguments passed to `f`.

- directional:

  Some comparison functions are commutative, so that
  `f(a, b) == f(b, a)` (e.g.,
  [`jaccard_similarity`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md)).
  Other functions are directional, so that `f(a, b)` measures `a`'s
  borrowing from `b`, which may not be the same as `f(b, a)` (e.g.,
  [`ratio_of_matches`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md)).
  If `directional` is `FALSE`, then only the minimum number of
  comparisons will be made, i.e., the upper triangle of the matrix. If
  `directional` is `TRUE`, then both directional comparisons will be
  measured. In no case, however, will documents be compared to
  themselves, i.e., the diagonal of the matrix.

- progress:

  Display a progress bar while comparing documents.

## Value

A square matrix with dimensions equal to the length of the corpus, and
row and column names set by the names of the documents in the corpus. A
value of `NA` in the matrix indicates that a comparison was not made. In
cases of directional comparisons, then the comparison reported is
`f(row, column)`.

## See also

See these document comparison functions,
[`jaccard_similarity`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md),
[`ratio_of_matches`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md).

## Examples

``` r
dir <- system.file("extdata/legal", package = "textreuse")
corpus <- TextReuseCorpus(dir = dir)
names(corpus) <- filenames(names(corpus))

# A non-directional comparison
pairwise_compare(corpus, jaccard_similarity)
#>                ca1851-match ca1851-nomatch ny1850-match
#> ca1851-match             NA    0.003529412  0.534753363
#> ca1851-nomatch           NA             NA  0.003307607
#> ny1850-match             NA             NA           NA

# A directional comparison
pairwise_compare(corpus, ratio_of_matches, directional = TRUE)
#>                ca1851-match ca1851-nomatch ny1850-match
#> ca1851-match             NA     0.01395349  0.695431472
#> ca1851-nomatch  0.005502063             NA  0.005076142
#> ny1850-match    0.737276479     0.01395349           NA
```
