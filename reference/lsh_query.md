# Query a LSH cache for matches to a single document

This function retrieves the matches for a single document from an
`lsh_buckets` object created by
[`lsh`](https://docs.ropensci.org/textreuse/reference/lsh.md). See
[`lsh_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md)
to retrieve all pairs of matches.

## Usage

``` r
lsh_query(buckets, id)
```

## Arguments

- buckets:

  An `lsh_buckets` object created by
  [`lsh`](https://docs.ropensci.org/textreuse/reference/lsh.md).

- id:

  The document ID to find matches for.

## Value

An `lsh_candidates` data frame with matches to the document specified.

## See also

[`lsh`](https://docs.ropensci.org/textreuse/reference/lsh.md),
[`lsh_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md)

## Examples

``` r
dir <- system.file("extdata/legal", package = "textreuse")
minhash <- minhash_generator(200, seed = 235)
corpus <- TextReuseCorpus(dir = dir,
                          tokenizer = tokenize_ngrams, n = 5,
                          minhash_func = minhash)
buckets <- lsh(corpus, bands = 50)
lsh_query(buckets, "ny1850-match")
#> # A tibble: 1 × 2
#>   a            b           
#>   <chr>        <chr>       
#> 1 ny1850-match ca1851-match
```
