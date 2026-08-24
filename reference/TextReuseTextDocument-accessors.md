# Accessors for TextReuse objects

Accessor functions to read and write components of
[`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
and
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
objects.

## Usage

``` r
tokens(x)

tokens(x) <- value

hashes(x)

hashes(x) <- value

minhashes(x)

minhashes(x) <- value
```

## Arguments

- x:

  The object to access.

- value:

  The value to assign.

## Value

Either a vector or a named list of vectors.
