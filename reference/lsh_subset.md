# List of all candidates in a corpus

List of all candidates in a corpus

## Usage

``` r
lsh_subset(candidates)
```

## Arguments

- candidates:

  A data frame of candidate pairs from
  [`lsh_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md).

## Value

A character vector of document IDs from the candidate pairs, to be used
to subset the
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md).

## Examples

``` r
dir <- system.file("extdata/legal", package = "textreuse")
minhash <- minhash_generator(200, seed = 234)
corpus <- TextReuseCorpus(dir = dir,
                          tokenizer = tokenize_ngrams, n = 5,
                          minhash_func = minhash)
buckets <- lsh(corpus, bands = 50)
candidates <- lsh_candidates(buckets)
lsh_subset(candidates)
#> [1] "ca1851-match" "ny1850-match"
corpus[lsh_subset(candidates)]
#> TextReuseCorpus
#> Number of documents: 2 
#> hash_func : hash_string 
#> minhash_func : minhash 
#> tokenizer : tokenize_ngrams 
```
