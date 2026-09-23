# Locality sensitive hashing for minhash

Locality sensitive hashing (LSH) discovers potential matches among a
corpus of documents quickly, so that only likely pairs can be compared.

## Usage

``` r
lsh(x, bands, progress = interactive())
```

## Arguments

- x:

  A
  [`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
  or
  [`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md).

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

A data frame (with the additional class `lsh_buckets`), containing a
column with the document IDs and a column with their LSH signatures, or
buckets.

## Details

Locality sensitive hashing is a technique for detecting document
similarity that does not require pairwise comparisons. When comparing
pairs of documents, the number of pairs grows rapidly, so that only the
smallest corpora can be compared pairwise in a reasonable amount of
computation time. Locality sensitive hashing, on the other hand, takes a
document which has been tokenized and hashed using a minhash algorithm.
(See
[`minhash_generator`](https://docs.ropensci.org/textreuse/reference/minhash_generator.md).)
Each set of minhash signatures is then broken into bands comprised of a
certain number of rows. (For example, 200 minhash signatures might be
broken down into 20 bands each containing 10 rows.) Each band is then
hashed to a bucket. Documents with identical rows in a band will be
hashed to the same bucket. The likelihood that a document will be marked
as a potential duplicate is proportional to the number of bands and
inversely proportional to the number of rows in each band.

This function returns a data frame with the additional class
`lsh_buckets`. The LSH technique only requires that the signatures for
each document be calculated once. So it is possible, as long as one uses
the same minhash function and the same number of bands, to combine the
outputs from this function at different times. The output can thus be
treated as a kind of cache of LSH signatures.

To extract pairs of documents from the output of this function, see
[`lsh_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md).

## References

Jure Leskovec, Anand Rajaraman, and Jeff Ullman, *Mining of Massive
Datasets* (Cambridge University Press, 2011), ch. 3. See also Matthew
Casperson, "[Minhash for
Dummies](https://matthewcasperson.blogspot.com/2013/11/minhash-for-dummies.html)"
(November 14, 2013).

## See also

[`minhash_generator`](https://docs.ropensci.org/textreuse/reference/minhash_generator.md),
[`lsh_add`](https://docs.ropensci.org/textreuse/reference/lsh_add.md),
[`lsh_candidates`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md),
[`lsh_query`](https://docs.ropensci.org/textreuse/reference/lsh_query.md),
[`lsh_probability`](https://docs.ropensci.org/textreuse/reference/lsh_probability.md),
[`lsh_threshold`](https://docs.ropensci.org/textreuse/reference/lsh_probability.md)

## Examples

``` r
dir <- system.file("extdata/legal", package = "textreuse")
minhash <- minhash_generator(200, seed = 235)
corpus <- TextReuseCorpus(dir = dir,
                          tokenizer = tokenize_ngrams, n = 5,
                          minhash_func = minhash)
buckets <- lsh(corpus, bands = 50)
buckets
#> # A tibble: 150 × 2
#>    doc          buckets                         
#>    <chr>        <chr>                           
#>  1 ca1851-match af692f79ec4b385468884a7310754366
#>  2 ca1851-match 7c25ad33c10068ed1d00e4a497be465e
#>  3 ca1851-match b36543167c07507579ecabbe47675f5f
#>  4 ca1851-match 68c1a9136b1aaf612b6982cf65db4dd9
#>  5 ca1851-match 99239407d33e84499e9b7fde16f43948
#>  6 ca1851-match 0ccad6c986d21807e9554b0757f6d156
#>  7 ca1851-match c32331c5c97d4d6b78fff25131aed561
#>  8 ca1851-match caac15d4cafc556ea08288ead841fd40
#>  9 ca1851-match d5868fcdf1f11f33859f640ac51e1931
#> 10 ca1851-match 999835f346cf6af6bf68bd96543997cd
#> # ℹ 140 more rows
```
