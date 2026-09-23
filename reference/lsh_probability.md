# Probability that a candidate pair will be detected with LSH

Functions to help choose the correct parameters for the
[`lsh`](https://docs.ropensci.org/textreuse/reference/lsh.md) and
[`minhash_generator`](https://docs.ropensci.org/textreuse/reference/minhash_generator.md)
functions. Use `lsh_threshold` to determine the minimum Jaccard
similarity for two documents for them to likely be considered a match.
Use `lsh_probability` to determine the probability that a pair of
documents with a known Jaccard similarity will be detected.

## Usage

``` r
lsh_probability(h, b, s)

lsh_threshold(h, b)
```

## Arguments

- h:

  The number of minhash signatures.

- b:

  The number of LSH bands.

- s:

  The Jaccard similarity.

## Details

Locality sensitive hashing returns a list of possible matches for
similar documents. How likely is it that a pair of documents will be
detected as a possible match? If `h` is the number of minhash
signatures, `b` is the number of bands in the LSH function (implying
then that the number of rows `r = h / b`), and `s` is the actual Jaccard
similarity of the two documents, then the probability `p` that the two
documents will be marked as a candidate pair is given by this equation.

\$\$p = 1 - (1 - s^{r})^{b}\$\$

According to the [MMDS book
page](https://www.cambridge.org/core/books/mining-of-massive-datasets/C1B37BA2CBB8361B94FDD1C6F4E47922),
that equation approximates an S-curve. This implies that there is a
threshold (`t`) for `s` approximated by this equation.

\$\$t = \frac{1}{b}^{\frac{1}{r}}\$\$

## References

Jure Leskovec, Anand Rajaraman, and Jeff Ullman, *Mining of Massive
Datasets* (Cambridge University Press, 2011), ch. 3.

## Examples

``` r
# Threshold for default values
lsh_threshold(h = 200, b = 40)
#> [1] 0.4781762

# Probability for varying values of s
lsh_probability(h = 200, b = 40, s = .25)
#> [1] 0.03832775
lsh_probability(h = 200, b = 40, s = .50)
#> [1] 0.7191538
lsh_probability(h = 200, b = 40, s = .75)
#> [1] 0.9999803
```
