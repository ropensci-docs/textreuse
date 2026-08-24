# Hash a string to an integer

Hash a string to an integer

## Usage

``` r
hash_string(x)
```

## Arguments

- x:

  A character vector to be hashed.

## Value

A vector of integer hashes.

## Examples

``` r
s <- c("How", "many", "roads", "must", "a", "man", "walk", "down")
hash_string(s)
#> [1] -1265721719  -727342581 -1125663377   258658140   -11612900  1695112593
#> [7] -1411833952 -1120374007
```
