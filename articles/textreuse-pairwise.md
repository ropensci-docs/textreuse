# Pairwise comparisons for document similarity

The most straightforward way to compare documents within a corpus is to
compare each document to every other document.

First we will load the corpus and tokenize it with shingled n-grams.

``` r

library(textreuse)
dir <- system.file("extdata/ats", package = "textreuse")
corpus <- TextReuseCorpus(dir = dir, tokenizer = tokenize_ngrams, n = 5,
                          progress = FALSE)
```

We can use any of the comparison functions to compare two documents in
the corpus. (Note that these functions, when applied to documents,
compare their hashed tokens and not the tokens directly.)

``` r

jaccard_similarity(corpus[["remember00palm"]], 
                   corpus[["remembermeorholy00palm"]])
```

    ## [1] 0.7005667

The
[`pairwise_compare()`](https://docs.ropensci.org/textreuse/reference/pairwise_compare.md)
function applies a comparison function to each pair of documents in a
corpus. The result is a matrix with the scores for each comparison.

``` r

comparisons <- pairwise_compare(corpus, jaccard_similarity, progress = FALSE)
comparisons[1:4, 1:4]
```

    ##                        calltounconv00baxt gospeltruth00whit
    ## calltounconv00baxt                     NA             0.001
    ## gospeltruth00whit                      NA                NA
    ## lifeofrevrichard00baxt                 NA                NA
    ##                        lifeofrevrichard00baxt
    ## calltounconv00baxt                      0.281
    ## gospeltruth00whit                       0.000
    ## lifeofrevrichard00baxt                     NA

If you prefer, you can convert the matrix of all comparisons to a data
frame of pairs and scores. Here we create the data frame and keep only
the pairs with scores above a significant value.

``` r

candidates <- pairwise_candidates(comparisons)
candidates[candidates$score > 0.1, ]
```

    ##                        a                      b     score
    ## 2     calltounconv00baxt lifeofrevrichard00baxt 0.2807068
    ## 26 practicalthought00nev thoughtsonpopery00nevi 0.4629759
    ## 21        remember00palm remembermeorholy00palm 0.7005667

The pairwise comparison method is inadequate for a corpus of any size,
however. For a corpus of size $`n`$, the number of comparisons (assuming
the comparisons are commutative) is $`\frac{n^2 - n}{2}`$. A corpus of
100 documents would require 4,950 comparisons; a corpus of 1,000
documents would require 499,500 comparisons. A better approach for
corpora of any appreciable size is to use the minhash/LSH algorithms
described in another vignette:

``` r

vignette("minhash", package = "textreuse")
```
