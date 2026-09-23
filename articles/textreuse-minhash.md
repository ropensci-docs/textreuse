# Minhash and locality-sensitive hashing

Performing pairwise comparisons in a corpus is time-consuming because
the number of comparisons grows geometrically with the size of the
corpus. Most of those comparisons, furthermore, are unnecessary because
they do not result in matches. The combination of minhash and
locality-sensitive hashing (LSH) seeks to solve these problems. They
make it possible to compute possible matches only once for each
document, so that the cost of computation grows linearly rather than
exponentially. This vignette explains how to use the minhash and
locality-sensitive hashing functions in this package. For an explanation
of why they work, see Jure Leskovec, Anand Rajaraman, and Jeff Ullman,
*Mining of Massive Datasets* (Cambridge University Press, 2011), ch. 3.
(This [blog
post](https://matthewcasperson.blogspot.com/2013/11/minhash-for-dummies.html)
is a more succinct explanation.)

We begin by creating a minhash function. A minhash function converts
tokenized text into a set of hash integers, then selects the minimum
value. This is the equivalent of randomly selecting a token. The
function then does the same thing repeatedly with different hashing
functions, in effect selecting `n` random shingles. The additional
hashing functions come from a bitwise XOR with random integers. That is
why the
[`minhash_generator()`](https://docs.ropensci.org/textreuse/reference/minhash_generator.md)
accepts a seed, so that we can re-create the same minhash function
again. In other words, a minhash function converts a set of tokens of
any length into `n` randomly selected and hashed tokens.

``` r

library(textreuse)
minhash <- minhash_generator(n = 240, seed = 3552)
head(minhash(c("turn tokens into", "tokens into hashes", "into hashes fast")))
```

    ## [1]  -358797036 -2024743034  -564447476 -1531354439  -614563502 -1888904030

Now when we load our corpus, we will tokenize our texts as usual, but we
will use our generated `minhash()` function to compute the hashes. We
specify that we want to create a minhash signature by passing our
minhash function to the `minhash_func =` parameter.

``` r

dir <- system.file("extdata/ats", package = "textreuse")
corpus <- TextReuseCorpus(dir = dir, tokenizer = tokenize_ngrams, n = 5,
                          minhash_func = minhash, keep_tokens = TRUE,
                          progress = FALSE)
```

We can verify that we have minhashes in our corpus:

``` r

head(minhashes(corpus[[1]]))
```

    ## [1] -2147434479 -2147455446 -2147434202 -2147464344 -2147438038 -2147483506

``` r

length(minhashes(corpus[[1]]))
```

    ## [1] 240

Now all our documents are represented by `n = 240` randomly selected and
hashed shingles. Comparing those shingles should be the equivalent of
finding the Jaccard similarity of the two documents. However, we still
have the problem of pairwise comparison.

The locality-sensitive hashing algorithm, provided in this package by
the [`lsh()`](https://docs.ropensci.org/textreuse/reference/lsh.md)
function, solves this problem. LSH breaks the minhashes into a series of
bands comprised of rows. For example, 200 minhashes might broken into 50
bands of 4 rows each. Each band is hashed to a bucket. If two documents
have the exact same minhashes in a band, they will be hashed to the same
bucket, and so will be considered candidate pairs. Each pair of
documents has as many chances to be considered a candidate as their are
bands, and the fewer rows there are in each band, the more likely it is
that each document will match another.

How likely is it, then, that we will detect a match? The probability of
a match depends on the Jaccard similarity of a pair of documents. The
more similar two documents are, the more likely they are to be
considered candidates, which is what we want. The probability of a match
is an S-curve (see Leskovec, Rajaraman, and Ullman), so there is a
threshold Jaccard similarity above which documents are likely to be a
match. We can calculate the likely threshold based on the number of
minhashes and bands that we are using.

``` r

lsh_threshold(h = 200, b = 50)
```

    ## [1] 0.3760603

``` r

lsh_threshold(h = 240, b = 80)
```

    ## [1] 0.2320794

Using 240 minhashes and 80 bands, we will likely detect documents with
an actual Jaccard similarity of above 0.232. We can also estimate the
probability that a pair of documents with a Jaccard similarity `s` will
be marked as potential matches.

``` r

lsh_probability(h = 240, b = 80, s = 0.25)
```

    ## [1] 0.7163087

``` r

lsh_probability(h = 240, b =  80, s = 0.75)
```

    ## [1] 1

These numbers seem reasonable for our purposes, so we will set the
number of minhashes at 240 and the number of bands at 80.

Now we can use the
[`lsh()`](https://docs.ropensci.org/textreuse/reference/lsh.md) function
to calculate the locality-sensitive hashes for our documents.

``` r

buckets <- lsh(corpus, bands = 80, progress = FALSE)
buckets
```

    ## # A tibble: 640 × 2
    ##    doc                buckets                         
    ##    <chr>              <chr>                           
    ##  1 calltounconv00baxt 9aa26fa70aad7ec5b12bd98ccdf6793e
    ##  2 calltounconv00baxt 4825fa9f8e4dacb42ff6e2fda9af7626
    ##  3 calltounconv00baxt ab2abb71ab0d908c075b578c8a5956ae
    ##  4 calltounconv00baxt 9b781ddba44d0d469f6176416adad845
    ##  5 calltounconv00baxt 8a4f14e7c000de114cb3847334ce2c04
    ##  6 calltounconv00baxt e0a6f8ad7f053d190348922d9532f28b
    ##  7 calltounconv00baxt d7a71d7cfc7185bb88fac50d99f8f04f
    ##  8 calltounconv00baxt 9149f5447fd633923053d364bc014f8d
    ##  9 calltounconv00baxt ce7a45e244a234c41e10d728db66faf8
    ## 10 calltounconv00baxt 226520d90e1bd80da4a6946e6cdbdf16
    ## # ℹ 630 more rows

Note that using the LSH method only requires us to calculate the
signatures (or buckets) for each document one time. This implies that we
can take several data frames of LSH signatures and bind their rows
together (e.g., with
[`dplyr::bind_rows()`](https://dplyr.tidyverse.org/reference/bind_rows.html)).
This permits us to compute the signatures for only part of a corpus at a
time, or to continue to add to the corpus. Note, however, that you
**must** use the same minhash function, generating the same number of
minhashes and using the same seed and you **must** use the same number
of bands in order to get valid results.

We can extract the potential matches from the cache using
[`lsh_query()`](https://docs.ropensci.org/textreuse/reference/lsh_query.md)
or
[`lsh_candidates()`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md).
The first function returns matches for only one document, specified by
its ID; the second functions returns all potential pairs of matches.

``` r

baxter_matches <- lsh_query(buckets, "calltounconv00baxt")
baxter_matches
```

    ## # A tibble: 1 × 2
    ##   a                  b                     
    ##   <chr>              <chr>                 
    ## 1 calltounconv00baxt lifeofrevrichard00baxt

``` r

candidates <- lsh_candidates(buckets)
candidates
```

    ## # A tibble: 3 × 3
    ##   a                     b                      score
    ##   <chr>                 <chr>                  <dbl>
    ## 1 calltounconv00baxt    lifeofrevrichard00baxt    NA
    ## 2 practicalthought00nev thoughtsonpopery00nevi    NA
    ## 3 remember00palm        remembermeorholy00palm    NA

Notice that LSH has identified the same three pairs of documents as
potential matches that we found with pairwise comparisons, but did so
much faster. But we do not have similarity scores; we only know that
these documents are likely to have Jaccard similarity scores above the
0.232 threshold.

Now we can use
[`lsh_compare()`](https://docs.ropensci.org/textreuse/reference/lsh_compare.md)
to apply a similarity function to the candidate pairs of documents. Note
that we only have to do 3 comparisons for all the candidates, instead of
28 pairs when comparing all 8 documents in the corpus pairwise.

``` r

lsh_compare(candidates, corpus, jaccard_similarity, progress = FALSE)
```

    ## # A tibble: 3 × 3
    ##   a                     b                      score
    ##   <chr>                 <chr>                  <dbl>
    ## 1 calltounconv00baxt    lifeofrevrichard00baxt 0.281
    ## 2 practicalthought00nev thoughtsonpopery00nevi 0.463
    ## 3 remember00palm        remembermeorholy00palm 0.701

Note that these results are identical to what we calculated in the
pairwise vignette, but required much less computation.
