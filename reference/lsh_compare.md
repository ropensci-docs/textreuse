# Compare candidates identified by LSH

The
[`lsh_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md)
only identifies potential matches, but cannot estimate the actual
similarity of the documents. This function takes a data frame returned
by
[`lsh_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md)
and applies a comparison function to each of the documents in a corpus,
thereby calculating the document similarity score. Note that since your
corpus will have minhash signatures rather than hashes for the tokens
itself, you will probably wish to use
[`tokenize`](https://docs.ropensci.org/textreuse/reference/tokenize.md)
to calculate new hashes. This can be done for just the potentially
similar documents. See the package vignettes for details.

## Usage

``` r
lsh_compare(candidates, corpus, f, progress = interactive())
```

## Arguments

- candidates:

  A data frame returned by
  [`lsh_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md).

- corpus:

  The same
  [`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
  corpus which was used to generate the candidates.

- f:

  A comparison function such as
  [`jaccard_similarity`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md).

- progress:

  Display a progress bar while comparing documents. Progress bars are
  disabled when using parallel processing.

## Value

A data frame with values calculated for `score`.

## Examples

``` r
dir <- system.file("extdata/legal", package = "textreuse")
minhash <- minhash_generator(200, seed = 234)
corpus <- TextReuseCorpus(dir = dir,
                          tokenizer = tokenize_ngrams, n = 5,
                          minhash_func = minhash)
buckets <- lsh(corpus, bands = 50)
candidates <- lsh_candidates(buckets)
lsh_compare(candidates, corpus, jaccard_similarity)
#> # A tibble: 1 × 3
#>   a            b            score
#>   <chr>        <chr>        <dbl>
#> 1 ca1851-match ny1850-match 0.450
```
