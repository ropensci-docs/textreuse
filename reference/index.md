# Package index

## All functions

- [`TextReuseCorpus()`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
  [`is.TextReuseCorpus()`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
  [`skipped()`](https://docs.ropensci.org/textreuse/reference/TextReuseCorpus.md)
  : TextReuseCorpus
- [`tokens()`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument-accessors.md)
  [`` `tokens<-`() ``](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument-accessors.md)
  [`hashes()`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument-accessors.md)
  [`` `hashes<-`() ``](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument-accessors.md)
  [`minhashes()`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument-accessors.md)
  [`` `minhashes<-`() ``](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument-accessors.md)
  : Accessors for TextReuse objects
- [`TextReuseTextDocument()`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
  [`is.TextReuseTextDocument()`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
  [`has_content()`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
  [`has_tokens()`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
  [`has_hashes()`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
  [`has_minhashes()`](https://docs.ropensci.org/textreuse/reference/TextReuseTextDocument.md)
  : TextReuseTextDocument
- [`align_local()`](https://docs.ropensci.org/textreuse/reference/align_local.md)
  : Local alignment of natural language texts
- [`as.matrix(`*`<textreuse_candidates>`*`)`](https://docs.ropensci.org/textreuse/reference/as.matrix.textreuse_candidates.md)
  [`as_sparse_matrix()`](https://docs.ropensci.org/textreuse/reference/as.matrix.textreuse_candidates.md)
  : Convert candidates data frames to other formats
- [`filenames()`](https://docs.ropensci.org/textreuse/reference/filenames.md)
  : Filenames from paths
- [`hash_string()`](https://docs.ropensci.org/textreuse/reference/hash_string.md)
  : Hash a string to an integer
- [`lsh()`](https://docs.ropensci.org/textreuse/reference/lsh.md) :
  Locality sensitive hashing for minhash
- [`lsh_add()`](https://docs.ropensci.org/textreuse/reference/lsh_add.md)
  : Add documents to a LSH cache
- [`lsh_candidates()`](https://docs.ropensci.org/textreuse/reference/lsh_candidates.md)
  : Candidate pairs from LSH comparisons
- [`lsh_compare()`](https://docs.ropensci.org/textreuse/reference/lsh_compare.md)
  : Compare candidates identified by LSH
- [`lsh_probability()`](https://docs.ropensci.org/textreuse/reference/lsh_probability.md)
  [`lsh_threshold()`](https://docs.ropensci.org/textreuse/reference/lsh_probability.md)
  : Probability that a candidate pair will be detected with LSH
- [`lsh_query()`](https://docs.ropensci.org/textreuse/reference/lsh_query.md)
  : Query a LSH cache for matches to a single document
- [`lsh_subset()`](https://docs.ropensci.org/textreuse/reference/lsh_subset.md)
  : List of all candidates in a corpus
- [`minhash_generator()`](https://docs.ropensci.org/textreuse/reference/minhash_generator.md)
  : Generate a minhash function
- [`pairwise_candidates()`](https://docs.ropensci.org/textreuse/reference/pairwise_candidates.md)
  : Candidate pairs from pairwise comparisons
- [`pairwise_compare()`](https://docs.ropensci.org/textreuse/reference/pairwise_compare.md)
  : Pairwise comparisons among documents in a corpus
- [`rehash()`](https://docs.ropensci.org/textreuse/reference/rehash.md)
  : Recompute the hashes for a document or corpus
- [`jaccard_similarity()`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md)
  [`jaccard_dissimilarity()`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md)
  [`jaccard_bag_similarity()`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md)
  [`ratio_of_matches()`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md)
  [`count_matches()`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md)
  [`matching_tokens()`](https://docs.ropensci.org/textreuse/reference/similarity-functions.md)
  : Measure similarity/dissimilarity in documents
- [`textreuse`](https://docs.ropensci.org/textreuse/reference/textreuse-package.md)
  [`textreuse-package`](https://docs.ropensci.org/textreuse/reference/textreuse-package.md)
  : textreuse: Detect Text Reuse and Document Similarity
- [`token_index()`](https://docs.ropensci.org/textreuse/reference/token_index.md)
  : Build an index of tokens and documents
- [`token_index_candidates()`](https://docs.ropensci.org/textreuse/reference/token_index_candidates.md)
  : Extract candidate document pairs from a token index
- [`tokenize()`](https://docs.ropensci.org/textreuse/reference/tokenize.md)
  : Recompute the tokens for a document or corpus
- [`tokenize_words()`](https://docs.ropensci.org/textreuse/reference/tokenizers.md)
  [`tokenize_sentences()`](https://docs.ropensci.org/textreuse/reference/tokenizers.md)
  [`tokenize_ngrams()`](https://docs.ropensci.org/textreuse/reference/tokenizers.md)
  [`tokenize_skip_ngrams()`](https://docs.ropensci.org/textreuse/reference/tokenizers.md)
  : Split texts into tokens
- [`wordcount()`](https://docs.ropensci.org/textreuse/reference/wordcount.md)
  : Count words
