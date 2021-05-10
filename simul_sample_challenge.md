Simulation / Random variables
================
Sebastian Knoche
04/27/2021

-   Idea: 10 samples, each of length 30
-   Each column in the matrix should be one sample

``` r
my.rnorm.vector <- rnorm(n = 10*30, mean = 0, sd = 1)
my.matrix <- matrix(my.rnorm.vector, nrow=30, ncol=10)
```

Inspecting the matrix

``` r
head(my.matrix)
```

    ##            [,1]       [,2]       [,3]       [,4]       [,5]       [,6]
    ## [1,]  0.6016792 -0.5525248 -0.1302036  0.8535568  1.0505577 -0.5862674
    ## [2,]  0.6480064 -0.6461241 -0.8432346 -1.3277050 -1.9308069 -1.9631742
    ## [3,]  0.7669977  0.9245384  0.4232141  0.6436551  1.3567295 -0.6013898
    ## [4,] -1.6090997  1.0501859 -0.8979006 -1.1971055 -1.1279902  0.6144528
    ## [5,] -1.6210965  0.4833939 -0.4421341  1.3326788 -0.1719718 -0.5198978
    ## [6,]  0.6030508  0.3504812 -0.4684999 -0.7622608 -1.8167508 -0.4471392
    ##            [,7]        [,8]        [,9]       [,10]
    ## [1,] -0.5184608 -1.40948205 -0.52418865 -0.08772709
    ## [2,]  0.9491626 -1.38317739 -1.87321310  0.73884094
    ## [3,]  2.0277667  0.05744666 -0.97425096  0.36742164
    ## [4,]  2.7223421  1.80959591  2.27013729 -1.63914087
    ## [5,] -0.2024283 -0.33175329 -0.21432800  0.09787144
    ## [6,] -0.9598231  0.50848954 -0.06725564 -0.07890310

#### Your Task:

Implement a function that takes the matrix as an input. The function
computes the mean and the sample variance for each sample and returns a
list of two elements.

``` r
my.fun.calc.summary <- function(tmp.matrix){
  my.mean <- apply(X = tmp.matrix, MARGIN = 2, FUN = mean)
  my.var <- apply(X = tmp.matrix, MARGIN = 2, FUN = var)
  tmp.list <- list(my.mean, my.var)
  names(tmp.list) <- c("Mean","Variance")
  return(tmp.list)
}
```

Checking

``` r
my.fun.calc.summary(my.matrix)
```

    ## $Mean
    ##  [1] -0.1334400039 -0.0009384463  0.0573365065  0.1131078733 -0.0751131812
    ##  [6] -0.2068016622  0.3321159037  0.0304579867  0.0816276003 -0.3926081924
    ## 
    ## $Variance
    ##  [1] 1.0628842 0.7934083 0.9466774 1.2343872 1.4697715 0.9299412 1.0024806
    ##  [8] 1.2433089 0.8543102 1.0865751

Checking further

``` r
my.result <- my.fun.calc.summary(my.matrix)
str(my.result)
```

    ## List of 2
    ##  $ Mean    : num [1:10] -0.13344 -0.000938 0.057337 0.113108 -0.075113 ...
    ##  $ Variance: num [1:10] 1.063 0.793 0.947 1.234 1.47 ...

#### Your Task II:

Implement a modified function that returns a matrix where the first
column is the column of means and the second is the column of variances.

``` r
my.fun.calc.summary.v2 <- function(tmp.matrix){
  tmp.list <- my.fun.calc.summary(tmp.matrix)
  tmp.result = matrix(c(tmp.list$Mean, tmp.list$Variance), ncol = length(tmp.list), byrow = FALSE)
  colnames(tmp.result) = names(tmp.list) #c("means","variances")
  return(tmp.result)
}
```

Checking

``` r
my.fun.calc.summary.v2(my.matrix)
```

    ##                Mean  Variance
    ##  [1,] -0.1334400039 1.0628842
    ##  [2,] -0.0009384463 0.7934083
    ##  [3,]  0.0573365065 0.9466774
    ##  [4,]  0.1131078733 1.2343872
    ##  [5,] -0.0751131812 1.4697715
    ##  [6,] -0.2068016622 0.9299412
    ##  [7,]  0.3321159037 1.0024806
    ##  [8,]  0.0304579867 1.2433089
    ##  [9,]  0.0816276003 0.8543102
    ## [10,] -0.3926081924 1.0865751

#### Your Task III:

Up to a now the simulated data is static. Write a function my.simulation
that has two arguments for the sample size and the number of samples.
This first first generates the data and then calls your summary function
to compute the summaries.

> Idea: 10 samples, each of length 30 Each column in the matrix should
> be one sample

``` r
my.simulation <- function(nr.sample = 10, size=30){
  my.rnorm.vector <- rnorm(n = nr.sample * size, mean = 0, sd = 1)
  my.matrix <- matrix(my.rnorm.vector, nrow = size, ncol = nr.sample)
  
  my.fun.calc.summary.v2(my.matrix)
}
```

Checking

``` r
my.simulation(nr.sample = 4, size=30)
```

    ##             Mean  Variance
    ## [1,]  0.20701409 0.8669880
    ## [2,] -0.30532619 0.7405912
    ## [3,] -0.11140379 1.0650900
    ## [4,] -0.07205448 1.0033179

``` r
my.simulation(nr.sample = 4, size=30)
```

    ##              Mean  Variance
    ## [1,]  0.049399046 1.0890784
    ## [2,] -0.002363007 0.9867662
    ## [3,]  0.065478523 1.2143560
    ## [4,] -0.122167327 1.1566023

``` r
my.simulation()
```

    ##               Mean  Variance
    ##  [1,] -0.038285169 1.2037201
    ##  [2,] -0.381379008 1.2098522
    ##  [3,]  0.256172392 0.9601983
    ##  [4,] -0.006456436 0.9733904
    ##  [5,]  0.080250212 0.5898549
    ##  [6,] -0.344905899 0.6798784
    ##  [7,] -0.052791665 1.2715367
    ##  [8,] -0.014743634 0.9924080
    ##  [9,] -0.243992131 0.9812502
    ## [10,]  0.215376159 1.4579705
