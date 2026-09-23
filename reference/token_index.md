# Build an index of tokens and documents

Build an inverted index from tokens to the documents that contain them.
This is useful for finding document pairs that share one or more n-grams
without comparing every document pair. The corpus must be created with
`keep_tokens = TRUE`.

## Usage

``` r
token_index(corpus, min_doc_count = 2, max_doc_count = Inf)
```

## Arguments

- corpus:

  A
  [`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
  with retained tokens.

- min_doc_count:

  Minimum number of documents a token must appear in to be retained.
  Increase this to remove rare tokens.

- max_doc_count:

  Maximum number of documents a token may appear in to be retained.
  Decrease this to remove very common tokens.

## Value

A `textreuse_token_index` data frame with columns `token`, `docs`, and
`n_docs`.
