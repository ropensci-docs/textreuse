# Split texts into tokens

These functions each turn a text into tokens. The `tokenize_ngrams`
functions returns shingled n-grams.

## Usage

``` r
tokenize_words(string, lowercase = TRUE)

tokenize_sentences(string, lowercase = TRUE)

tokenize_ngrams(string, lowercase = TRUE, n = 3)

tokenize_skip_ngrams(string, lowercase = TRUE, n = 3, k = 1)
```

## Arguments

- string:

  A character vector of length 1 to be tokenized.

- lowercase:

  Should the tokens be made lower case?

- n:

  For n-gram tokenizers, the number of words in each n-gram.

- k:

  For the skip n-gram tokenizer, the maximum skip distance between
  words. The function will compute all skip n-grams between `0` and `k`.

## Value

A character vector containing the tokens.

## Details

These functions will strip all punctuation.

## Examples

``` r
dylan <- "How many roads must a man walk down? The answer is blowin' in the wind."
tokenize_words(dylan)
#>  [1] "how"    "many"   "roads"  "must"   "a"      "man"    "walk"   "down"  
#>  [9] "the"    "answer" "is"     "blowin" "in"     "the"    "wind"  
tokenize_sentences(dylan)
#> [1] "how many roads must a man walk down" "the answer is blowin in the wind"   
tokenize_ngrams(dylan, n = 2)
#>  [1] "how many"   "many roads" "roads must" "must a"     "a man"     
#>  [6] "man walk"   "walk down"  "down the"   "the answer" "answer is" 
#> [11] "is blowin"  "blowin in"  "in the"     "the wind"  
tokenize_skip_ngrams(dylan, n = 3, k = 2)
#>  [1] "how must walk"      "many a down"        "roads man the"     
#>  [4] "must walk answer"   "a down is"          "man the blowin"    
#>  [7] "walk answer in"     "down is the"        "the blowin wind"   
#> [10] "how roads a"        "many must man"      "roads a walk"      
#> [13] "must man down"      "a walk the"         "man down answer"   
#> [16] "walk the is"        "down answer blowin" "the is in"         
#> [19] "answer blowin the"  "is in wind"         "how many roads"    
#> [22] "many roads must"    "roads must a"       "must a man"        
#> [25] "a man walk"         "man walk down"      "walk down the"     
#> [28] "down the answer"    "the answer is"      "answer is blowin"  
#> [31] "is blowin in"       "blowin in the"      "in the wind"       
```
