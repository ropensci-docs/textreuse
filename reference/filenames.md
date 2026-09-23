# Filenames from paths

This function takes a character vector of paths and returns just the
file name, by default without the extension. A
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
uses the paths to the files in the corpus as the names of the list. This
function is intended to turn those paths into more manageable
identifiers.

## Usage

``` r
filenames(paths, extension = FALSE)
```

## Arguments

- paths:

  A character vector of paths.

- extension:

  Should the file extension be preserved?

## See also

[`basename`](https://rdrr.io/r/base/basename.html)

## Examples

``` r
paths <- c("corpus/one.txt", "corpus/two.md", "corpus/three.text")
filenames(paths)
#> [1] "one"   "two"   "three"
filenames(paths, extension = TRUE)
#> [1] "one.txt"    "two.md"     "three.text"
```
