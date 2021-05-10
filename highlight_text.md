Highlight Text
================
Sebastian Knoche
04/14/2021

function for highlighting text

``` r
best_practice <- c("Write", "programs", "for", "people", "not", "computers")
asterisk <- "***"
```

> R interprets a variable with a single value as a vector with one
> element.

``` r
highlight <- function(input, markings){
  output <- c(markings, input, markings)  # Alternative: cat, paste
  return(output)
}
highlight(best_practice, asterisk)
```

    ## [1] "***"       "Write"     "programs"  "for"       "people"    "not"      
    ## [7] "computers" "***"
