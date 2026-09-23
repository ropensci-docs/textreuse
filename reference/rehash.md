# Recompute the hashes for a document or corpus

Given a
[`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
or a
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md),
this function recomputes either the hashes or the minhashes with the
function specified. This implies that you have retained the tokens with
the `keep_tokens = TRUE` parameter.

## Usage

``` r
rehash(x, func, type = c("hashes", "minhashes"))
```

## Arguments

- x:

  A
  [`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
  or
  [`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md).

- func:

  A function to either hash the tokens or to generate the minhash
  signature. See
  [`hash_string`](https://docs.ropensci.org/textreuse/reference/hash_string.md),
  [`minhash_generator`](https://docs.ropensci.org/textreuse/reference/minhash_generator.md).

- type:

  Recompute the `hashes` or `minhashes`?

## Value

The modified
[`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
or
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md).

## Examples

``` r
dir <- system.file("extdata/legal", package = "textreuse")
minhash1 <- minhash_generator(seed = 1)
corpus <- TextReuseCorpus(dir = dir, minhash_func = minhash1, keep_tokens = TRUE)
head(minhashes(corpus[[1]]))
#> [1] -2123034802 -2135950804 -2141005830 -2143887934 -2140211929 -2141513215
minhash2 <- minhash_generator(seed = 2)
corpus <- rehash(corpus, minhash2, type = "minhashes")
head(minhashes(corpus[[2]]))
#> [1] -2139907006 -2113028606 -2143609422 -2087210065 -2050121581 -2049620020
```
