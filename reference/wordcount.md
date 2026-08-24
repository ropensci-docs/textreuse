# Count words

This function counts words in a text, for example, a character vector, a
[`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md),
some other object that inherits from
[`TextDocument`](https://rdrr.io/pkg/NLP/man/TextDocument.html), or a
all the documents in a
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md).

## Usage

``` r
wordcount(x)
```

## Arguments

- x:

  The object containing a text.

## Value

An integer vector for the word count.
