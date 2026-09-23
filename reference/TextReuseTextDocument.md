# TextReuseTextDocument

This is the constructor function for `TextReuseTextDocument` objects.
This class is used for comparing documents.

## Usage

``` r
TextReuseTextDocument(
  text,
  file = NULL,
  meta = list(),
  tokenizer = tokenize_ngrams,
  ...,
  hash_func = hash_string,
  minhash_func = NULL,
  keep_tokens = FALSE,
  keep_text = TRUE,
  skip_short = TRUE,
  encoding = "unknown"
)

is.TextReuseTextDocument(x)

has_content(x)

has_tokens(x)

has_hashes(x)

has_minhashes(x)
```

## Arguments

- text:

  A character vector containing the text of the document. This argument
  can be skipped if supplying `file`.

- file:

  The path to a text file, if `text` is not provided.

- meta:

  A list with named elements for the metadata associated with this
  document. If a document is created using the `text` parameter, then
  you must provide an `id` field, e.g., `meta = list(id = "my_id")`. If
  the document is created using `file`, then the ID will be created from
  the file name.

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

  Should the tokens be saved in the document that is returned or
  discarded?

- keep_text:

  Should the text be saved in the document that is returned or
  discarded?

- skip_short:

  Should short documents be skipped? (See details.)

- encoding:

  Encoding to be used when reading files.

- x:

  An R object to check.

## Value

An object of class `TextReuseTextDocument`. This object inherits from
the virtual S3 class
[`TextDocument`](https://rdrr.io/pkg/NLP/man/TextDocument.html) in the
NLP package. It contains the following elements:

- content:

  The text of the document.

- tokens:

  The tokens created from the text.

- hashes:

  Hashes created from the tokens.

- minhashes:

  The minhash signature of the document.

- metadata:

  The document metadata, including the filename (if any) in `file`.

## Details

This constructor function follows a three-step process. It reads in the
text, either from a file or from memory. It then tokenizes that text.
Then it hashes the tokens. Most of the comparison functions in this
package rely only on the hashes to make the comparison. By passing
`FALSE` to `keep_tokens` and `keep_text`, you can avoid saving those
objects, which can result in significant memory savings for large
corpora.

If `skip_short = TRUE`, this function will return `NULL` for very short
or empty documents. A very short document is one where there are too few
words to create at least two n-grams. For example, if five-grams are
desired, then a document must be at least six words long. If no value of
`n` is provided, then the function assumes a value of `n = 3`. A warning
will be printed with the document ID of a skipped document.

## See also

[Accessors for TextReuse
objects](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument-accessors.md).

## Examples

``` r
file <- system.file("extdata/legal/ny1850-match.txt", package = "textreuse")
doc  <- TextReuseTextDocument(file = file, meta = list(id = "ny1850"))
print(doc)
#> TextReuseTextDocument
#> file : /github/home/R/x86_64-pc-linux-gnu-library/4.6/textreuse/extdata/legal/ny1850-match.txt 
#> hash_func : hash_string 
#> id : ny1850 
#> tokenizer : tokenize_ngrams 
#> content : § 597. Every action must be prosecuted in the name
#> of the real party in interest, except as otherwise provided in section 599.
#> 
#> ..a—
#> 
#> 5./imended Code, § 111.
#> 
#> §598. In the case of an assignment of a t
meta(doc)
#> $file
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/textreuse/extdata/legal/ny1850-match.txt"
#> 
#> $hash_func
#> [1] "hash_string"
#> 
#> $id
#> [1] "ny1850"
#> 
#> $tokenizer
#> [1] "tokenize_ngrams"
#> 
head(tokens(doc))
#> NULL
head(hashes(doc))
#> [1]  -221637926   996319810  -419169523   -37457565 -1872322441    75599962
if (FALSE) { # \dontrun{
content(doc)
} # }
```
