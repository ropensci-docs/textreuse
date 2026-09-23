# TextReuseCorpus

This is the constructor function for a `TextReuseCorpus`, modeled on the
virtual S3 class `Corpus` from the `tm` package. The object is a
`TextReuseCorpus`, which is basically a list containing objects of class
[`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md).
Arguments are passed along to that constructor function. To create the
corpus, you can pass either a character vector of paths to text files
using the `paths =` parameter, a directory containing text files (with
any extension) using the `dir =` parameter, or a character vector of
documents using the `text = ` parameter, where each element in the
characer vector is a document. If the character vector passed to
`text = ` has names, then those names will be used as the document IDs.
Otherwise, IDs will be assigned to the documents. Only one of the
`paths`, `dir`, or `text` parameters should be specified.

## Usage

``` r
TextReuseCorpus(
  paths,
  dir = NULL,
  text = NULL,
  meta = list(),
  progress = interactive(),
  tokenizer = tokenize_ngrams,
  ...,
  hash_func = hash_string,
  minhash_func = NULL,
  keep_tokens = FALSE,
  keep_text = TRUE,
  skip_short = TRUE,
  encoding = "unknown"
)

is.TextReuseCorpus(x)

skipped(x)
```

## Arguments

- paths:

  A character vector of paths to files to be opened.

- dir:

  The path to a directory of text files.

- text:

  A character vector (possibly named) of documents.

- meta:

  A list with named elements for the metadata associated with this
  corpus.

- progress:

  Display a progress bar while loading files.

- tokenizer:

  A function to split the text into tokens. See
  [`tokenizers`](https://docs.ropensci.org/textreuse/reference/tokenizers.md).
  If value is `NULL`, then tokenizing and hashing will be skipped.

- ...:

  Arguments passed on to the `tokenizer`.

- hash_func:

  A function to hash the tokens. See
  [`hash_string`](https://docs.ropensci.org/textreuse/reference/hash_string.md).

- minhash_func:

  A function to create minhash signatures of the document. See
  [`minhash_generator`](https://docs.ropensci.org/textreuse/reference/minhash_generator.md).

- keep_tokens:

  Should the tokens be saved in the documents that are returned or
  discarded?

- keep_text:

  Should the text be saved in the documents that are returned or
  discarded?

- skip_short:

  Should short documents be skipped? (See details.)

- encoding:

  Encoding to be used when reading files.

- x:

  An R object to check.

## Details

If `skip_short = TRUE`, this function will skip very short or empty
documents. A very short document is one where there are too few words to
create at least two n-grams. For example, if five-grams are desired,
then a document must be at least six words long. If no value of `n` is
provided, then the function assumes a value of `n = 3`. A warning will
be printed with the document ID of each skipped document. Use
`skipped()` to get the IDs of skipped documents.

This function will use multiple cores on non-Windows machines if the
`"mc.cores"` option is set. For example, to use four cores:
`options("mc.cores" = 4L)`.

## See also

[Accessors for TextReuse
objects](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument-accessors.md).

## Examples

``` r
dir <- system.file("extdata/legal", package = "textreuse")
corpus <- TextReuseCorpus(dir = dir, meta = list("description" = "Field Codes"))
# Subset by position or file name
corpus[[1]]
#> TextReuseTextDocument
#> file : /github/home/R/x86_64-pc-linux-gnu-library/4.6/textreuse/extdata/legal/ca1851-match.txt 
#> hash_func : hash_string 
#> id : ca1851-match 
#> minhash_func : 
#> tokenizer : tokenize_ngrams 
#> content : § 4. Every action shall be prosecuted in the name of the real party
#> in interest, except as otherwise provided in this Act.
#> 
#> § 5. In the case of an assignment of a thing in action, the action by
#> the as
names(corpus)
#> [1] "ca1851-match"   "ca1851-nomatch" "ny1850-match"  
corpus[["ca1851-match"]]
#> TextReuseTextDocument
#> file : /github/home/R/x86_64-pc-linux-gnu-library/4.6/textreuse/extdata/legal/ca1851-match.txt 
#> hash_func : hash_string 
#> id : ca1851-match 
#> minhash_func : 
#> tokenizer : tokenize_ngrams 
#> content : § 4. Every action shall be prosecuted in the name of the real party
#> in interest, except as otherwise provided in this Act.
#> 
#> § 5. In the case of an assignment of a thing in action, the action by
#> the as
```
