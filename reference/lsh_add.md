# Add documents to a LSH cache

This function adds buckets for one or more new documents to an existing
`lsh_buckets` object. Use the same `bands` value and minhash function
that were used to create the original buckets.

## Usage

``` r
lsh_add(buckets, x, bands, progress = interactive())
```

## Arguments

- buckets:

  An `lsh_buckets` object created by
  [`lsh`](https://docs.ropensci.org/textreuse/reference/lsh.md).

- x:

  A
  [`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
  or
  [`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
  with minhashes.

- bands:

  The number of bands to use for locality sensitive hashing. The number
  of hashes in the documents in the corpus must be evenly divisible by
  the number of bands. See
  [`lsh_threshold`](https://docs.ropensci.org/textreuse/reference/lsh_probability.md)
  and
  [`lsh_probability`](https://docs.ropensci.org/textreuse/reference/lsh_probability.md)
  for guidance in selecting the number of bands and hashes.

- progress:

  Display a progress bar while comparing documents.

## Value

An updated `lsh_buckets` object.

## See also

[`lsh`](https://docs.ropensci.org/textreuse/reference/lsh.md),
[`lsh_query`](https://docs.ropensci.org/textreuse/reference/lsh_query.md),
[`lsh_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md)
