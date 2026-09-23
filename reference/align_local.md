# Local alignment of natural language texts

This function takes two texts, either as strings or as
`TextReuseTextDocument` objects, and finds the optimal local alignment
of those texts. A local alignment finds the best matching subset of the
two documents. This function adapts the [Smith-Waterman
algorithm](https://en.wikipedia.org/wiki/Smith-Waterman_algorithm), used
for genetic sequencing, for use with natural language. It compare the
texts word by word (the comparison is case-insensitive) and scores them
according to a set of parameters. These parameters define the score for
a `match`, and the penalties for a `mismatch` and for opening a `gap`
(i.e., the first mismatch in a potential sequence). The function then
reports the optimal local alignment. Only the subset of the documents
that is a match is included. Insertions or deletions in the text are
reported with the `edit_mark` character.

## Usage

``` r
align_local(
  a,
  b,
  match = 2L,
  mismatch = -1L,
  gap = -1L,
  edit_mark = "#",
  preserve_punctuation = FALSE,
  progress = interactive()
)
```

## Arguments

- a:

  A character vector of length one, or a
  [`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md).

- b:

  A character vector of length one, or a
  [`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md).

- match:

  The score to assign a matching word. Should be a positive integer.

- mismatch:

  The score to assign a mismatching word. Should be a negative integer
  or zero.

- gap:

  The penalty for opening a gap in the sequence. Should be a negative
  integer or zero.

- edit_mark:

  A single character used for displaying for displaying
  insertions/deletions in the documents.

- preserve_punctuation:

  Preserve punctuation in the displayed alignment. The alignment still
  compares tokens after stripping punctuation.

- progress:

  Display a progress bar and messages while computing the alignment.

## Value

A list with the class `textreuse_alignment`. This list contains several
elements:

- `a_edit` and `b_edit`: Character vectors of the sequences with edits
  marked.

- `score`: The score of the optimal alignment.

## Details

The compute time of this function is proportional to the product of the
lengths of the two documents. Thus, longer documents will take
considerably more time to compute. This function has been tested with
pairs of documents containing about 25 thousand words each.

If the function reports that there were multiple optimal alignments,
then it is likely that there is no strong match in the document.

The score reported for the local alignment is dependent on both the size
of the documents and on the strength of the match, as well as on the
parameters for match, mismatch, and gap penalties, so the scores are not
directly comparable.

## References

For a useful description of the algorithm, see [this
post](https://www.etherealbits.com/2013/04/string-alignment-dynamic-programming-dna/).
For the application of the Smith-Waterman algorithm to natural language,
see David A. Smith, Ryan Cordell, and Elizabeth Maddock Dillon,
"Infectious Texts: Modeling Text Reuse in Nineteenth-Century
Newspapers," IEEE International Conference on Big Data, 2013.

## Examples

``` r
align_local("The answer is blowin' in the wind.",
            "As the Bob Dylan song says, the answer is blowing in the wind.")
#> TextReuse alignment
#> Alignment score: 11 
#> Document A:
#> The answer is blowin ####### in the wind
#> 
#> Document B:
#> the answer is ###### blowing in the wind
#> 

# Example of matching documents from a corpus
dir <- system.file("extdata/legal", package = "textreuse")
corpus <- TextReuseCorpus(dir = dir, progress = FALSE)
alignment <- align_local(corpus[["ca1851-match"]], corpus[["ny1850-match"]])
str(alignment)
#> List of 3
#>  $ a_edits: chr "Every action shall #### be prosecuted in the name of the real party in interest except as otherwise provided in"| __truncated__
#>  $ b_edits: chr "Every action ##### must be prosecuted in the name of the real party in interest except as otherwise provided in"| __truncated__
#>  $ score  : int 1035
#>  - attr(*, "class")= chr [1:2] "textreuse_alignment" "list"
```
