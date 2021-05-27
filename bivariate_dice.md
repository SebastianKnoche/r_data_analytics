---
title: "Bivariate Dice"
author: "Sebastian Knoche"
date: "2021-05-10"
output:
  html_document:
    keep_md: yes
  pdf_document: default
---



### Bivariate probability distribution
Write a function `my.bivariate.dice` which rolls two dice `Nsample` times 
and computes the sum of the two dice. The arguments are:

* `die1` the elements of the first die with default 1, ... , 6
* `die2` the elements of the first die with default 1, ... , 6
* `prob1` the vector of probabilities for the first die, with default `NULL`
* `prob2` the vector of probabilities for the first die, with default `NULL`
* `Nsample` sample size with default 20


```r
my_bivariate_dice <- function( die_1 = 1:6,
                               die_2 = 1:6,
                               prob_1 = NULL,
                               prob_2 = NULL,
                               n_sample = 20 ){

  tmp_die_1 <- sample(die_1, n_sample, replace = TRUE, prob = prob_1)
  tmp_die_2 <- sample(die_2, n_sample, replace = TRUE, prob = prob_2)
  tmp_sum <- tmp_die_1 + tmp_die_2
  return(tmp_sum)
}
```
> Note: `missing(x)` will test whether an argument `x` within a function has been specified within the call.


### Monte Carlo
Write a function `my.bivariate.dice.matrix` which simulates the previous
experiment `Nreps` times. The function has one additional input argument
`Nreps` governing the number of repetitions. The output of the function is a
matrix where each columns is one sample (of size `Nsample`).


```r
my_bivariate_dice_matrix <- function( n_reps = 2,
                                      die_1 = 1:6,
                                      die_2 = 1:6,
                                      prob_1 = NULL,
                                      prob_2 = NULL,
                                      n_sample = 20 ){

  tmp_mtx <- matrix(NA, nrow = n_sample, ncol = n_reps)
  for(i in 1:n_reps){
    tmp_mtx[, i] <- my_bivariate_dice(die_1, die_2,prob_1, prob_2, n_sample)
  }
  return(tmp_mtx)
}
```


```r
my_bivariate_dice_matrix(n_reps = 4, n_sample = 10)
```

```
##       [,1] [,2] [,3] [,4]
##  [1,]    4    6   11    8
##  [2,]    9    3    9    5
##  [3,]    5    9    2    7
##  [4,]    5    6    6    6
##  [5,]    6    7   10    8
##  [6,]    8    9    6    7
##  [7,]    8    7    3    7
##  [8,]   10   12    8    8
##  [9,]   12    7    2    9
## [10,]    5    9   10    8
```
