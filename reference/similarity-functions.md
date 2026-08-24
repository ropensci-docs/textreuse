# Measure similarity/dissimilarity in documents

A set of functions which take two sets or bag of words and measure their
similarity or dissimilarity.

## Usage

``` r
jaccard_similarity(a, b)

jaccard_dissimilarity(a, b)

jaccard_bag_similarity(a, b)

ratio_of_matches(a, b)

count_matches(a, b)

matching_tokens(a, b)
```

## Arguments

- a:

  The first set (or bag) to be compared. The origin bag for directional
  comparisons.

- b:

  The second set (or bag) to be compared. The destination bag for
  directional comparisons.

## Details

The functions `jaccard_similarity` and `jaccard_dissimilarity` provide
the Jaccard measures of similarity or dissimilarity for two sets. The
coefficients will be numbers between `0` and `1`. For the similarity
coefficient, the higher the number the more similar the two sets are.
When applied to two documents of class
[`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md),
the hashes in those documents are compared. But this function can be
passed objects of any class accepted by the set functions in base R. So
it is possible, for instance, to pass this function two character
vectors comprised of word, line, sentence, or paragraph tokens, or those
character vectors hashed as integers.

The Jaccard similarity coeffecient is defined as follows:

\$\$J(A, B) = \frac{ \| A \cap B \| }{ \| A \cup B \| }\$\$

The Jaccard dissimilarity is simply

\$\$1 - J(A, B)\$\$

The function `jaccard_bag_similarity` treats `a` and `b` as bags rather
than sets, so that the result is a fraction where the numerator is the
sum of each matching element counted the minimum number of times it
appears in each bag, and the denominator is the sum of the lengths of
both bags. The maximum value for the Jaccard bag similarity is `0.5`.

The function `ratio_of_matches` finds the ratio between the number of
items in `b` that are also in `a` and the total number of items in `b`.
Note that this similarity measure is directional: it measures how much
`b` borrows from `a`, but says nothing about how much of `a` borrows
from `b`.

The function `count_matches` returns the numerator used by
`ratio_of_matches`: the number of items in `b` also found in `a`. The
function `matching_tokens` returns those matching items from `b`,
preserving their order and duplicates.

## References

Jure Leskovec, Anand Rajaraman, and Jeff Ullman, *Mining of Massive
Datasets* (Cambridge University Press, 2011).

## Examples

``` r
jaccard_similarity(1:6, 3:10)
#> [1] 0.4
jaccard_dissimilarity(1:6, 3:10)
#> [1] 0.6

a <- c("a", "a", "a", "b")
b <- c("a", "a", "b", "b", "c")
jaccard_similarity(a, b)
#> [1] 0.6666667
jaccard_bag_similarity(a, b)
#> [1] 0.3333333
ratio_of_matches(a, b)
#> [1] 0.8
ratio_of_matches(b, a)
#> [1] 1
count_matches(a, b)
#> [1] 4
matching_tokens(a, b)
#> [1] "a" "a" "b" "b"

ny         <- system.file("extdata/legal/ny1850-match.txt", package = "textreuse")
ca_match   <- system.file("extdata/legal/ca1851-match.txt", package = "textreuse")
ca_nomatch <- system.file("extdata/legal/ca1851-nomatch.txt", package = "textreuse")

ny         <- TextReuseTextDocument(file = ny,
                                    meta = list(id = "ny"))
ca_match   <- TextReuseTextDocument(file = ca_match,
                                    meta = list(id = "ca_match"))
ca_nomatch <- TextReuseTextDocument(file = ca_nomatch,
                                    meta = list(id = "ca_nomatch"))

# These two should have higher similarity scores
jaccard_similarity(ny, ca_match)
#> [1] 0.5347534
ratio_of_matches(ny, ca_match)
#> [1] 0.7372765

# These two should have lower similarity scores
jaccard_similarity(ny, ca_nomatch)
#> [1] 0.003307607
ratio_of_matches(ny, ca_nomatch)
#> [1] 0.01395349
```
