# Recompute the tokens for a document or corpus

Given a
[`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
or a
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md),
this function recomputes the tokens and hashes with the functions
specified. Optionally, it can also recompute the minhash signatures.

## Usage

``` r
tokenize(
  x,
  tokenizer,
  ...,
  hash_func = hash_string,
  minhash_func = NULL,
  keep_tokens = FALSE,
  keep_text = TRUE
)
```

## Arguments

- x:

  A
  [`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
  or
  [`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md).

- tokenizer:

  A function to split the text into tokens. See
  [`tokenizers`](https://docs.ropensci.org/textreuse/reference/tokenizers.md).

- ...:

  Arguments passed on to the `tokenizer`.

- hash_func:

  A function to hash the tokens. See
  [`hash_string`](https://docs.ropensci.org/textreuse/reference/hash_string.md).

- minhash_func:

  A function to create minhash signatures. See
  [`minhash_generator`](https://docs.ropensci.org/textreuse/reference/minhash_generator.md).

- keep_tokens:

  Should the tokens be saved in the document that is returned or
  discarded?

- keep_text:

  Should the text be saved in the document that is returned or
  discarded?

## Value

The modified
[`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
or
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md).

## Examples

``` r
dir <- system.file("extdata/legal", package = "textreuse")
corpus <- TextReuseCorpus(dir = dir, tokenizer = NULL)
corpus <- tokenize(corpus, tokenize_ngrams)
head(tokens(corpus[[1]]))
#> [1] "4 every action"      "every action shall"  "action shall be"    
#> [4] "shall be prosecuted" "be prosecuted in"    "prosecuted in the"  
```
