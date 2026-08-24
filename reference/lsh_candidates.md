# Candidate pairs from LSH comparisons

Given a data frame of LSH buckets returned from
[`lsh`](https://docs.ropensci.org/textreuse/reference/lsh.md), this
function returns the potential candidates.

## Usage

``` r
lsh_candidates(buckets)
```

## Arguments

- buckets:

  A data frame returned from
  [`lsh`](https://docs.ropensci.org/textreuse/reference/lsh.md).

## Value

A data frame of candidate pairs.

## Examples

``` r
dir <- system.file("extdata/legal", package = "textreuse")
minhash <- minhash_generator(200, seed = 234)
corpus <- TextReuseCorpus(dir = dir,
                          tokenizer = tokenize_ngrams, n = 5,
                          minhash_func = minhash)
buckets <- lsh(corpus, bands = 50)
lsh_candidates(buckets)
#> # A tibble: 1 × 3
#>   a            b            score
#>   <chr>        <chr>        <dbl>
#> 1 ca1851-match ny1850-match    NA
```
