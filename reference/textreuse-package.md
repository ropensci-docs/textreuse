# textreuse: Detect Text Reuse and Document Similarity

Tools for measuring similarity among documents and detecting passages
which have been reused. Implements shingled n-gram, skip n-gram, and
other tokenizers; similarity/dissimilarity functions; pairwise
comparisons; minhash and locality sensitive hashing algorithms; and a
version of the Smith-Waterman local alignment algorithm suitable for
natural language.

## Details

The best place to begin with this package in the introductory vignette.

[`vignette("textreuse-introduction", package = "textreuse")`](https://docs.ropensci.org/textreuse/articles/textreuse-introduction.md)

After reading that vignette, the "pairwise" and "minhash" vignettes
introduce specific paths for working with the package.

[`vignette("textreuse-pairwise", package = "textreuse")`](https://docs.ropensci.org/textreuse/articles/textreuse-pairwise.md)

[`vignette("textreuse-minhash", package = "textreuse")`](https://docs.ropensci.org/textreuse/articles/textreuse-minhash.md)

[`vignette("textreuse-alignment", package = "textreuse")`](https://docs.ropensci.org/textreuse/articles/textreuse-alignment.md)

Another good place to begin with the package is the documentation for
loading documents
([`TextReuseTextDocument`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
and
[`TextReuseCorpus`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)),
for
[tokenizers](https://docs.ropensci.org/textreuse/reference/tokenizers.md),
[similarity
functions](https://docs.ropensci.org/textreuse/reference/similarity-functions.md),
and [locality-sensitive
hashing](https://docs.ropensci.org/textreuse/reference/lsh.md).

## References

The sample data provided in the `extdata/ats` directory contains
nineteenth-century American Tract Society publications gathered from the
[Internet Archive](https://archive.org/).

The sample data provided in the `extdata/legal` directory, are taken
from the following nineteenth-century codes of civil procedure from
California and New York.

*Final Report of the Commissioners on Practice and Pleadings*, in 2
*Documents of the Assembly of New York*, 73rd Sess., No. 16, (1850):
243-250, sections 597-613. [Google
Books](https://books.google.com/books?id=9HEbAQAAIAAJ&pg=PA243#v=onepage&q&f=false).

*An Act To Regulate Proceedings in Civil Cases*, 1851 *California Laws*
51, 51-53 sections 4-17; 101, sections 313-316. [Google
Books](https://books.google.com/books?id=4PHEAAAAIAAJ&pg=PA51#v=onepage&q&f=false).

## See also

Useful links:

- <https://docs.ropensci.org/textreuse/>

- <https://github.com/ropensci/textreuse>

- Report bugs at <https://github.com/ropensci/textreuse/issues>

## Author

**Maintainer**: Yaoxiang Li <liyaoxiang@outlook.com>
([ORCID](https://orcid.org/0000-0001-9200-1016))

Authors:

- Yaoxiang Li <liyaoxiang@outlook.com>
  ([ORCID](https://orcid.org/0000-0001-9200-1016))

- Lincoln Mullen ([ORCID](https://orcid.org/0000-0001-5103-6917))
