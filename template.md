Homework 1
================
Alexey Abramov

This is my solution to HW1\!

``` r
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ──────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

# Problem 1

## Create a df with the specified elements:

``` r
prob1_df = 
  tibble(
    samp = rnorm(10),
    samp_gt_0 = samp > 0,
    char_vec = c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j"),
    factor_vec = factor(c("low", "low", "low", "low", "mod", "mod", "mod", "high", "high", "high"))
  )
```

## Take the mean of each variable in my data frame:

``` r
mean(pull(prob1_df, samp))
```

    ## [1] 0.04163491

``` r
mean(pull(prob1_df, samp_gt_0))
```

    ## [1] 0.3

``` r
mean(pull(prob1_df, char_vec))
```

    ## Warning in mean.default(pull(prob1_df, char_vec)): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

``` r
mean(pull(prob1_df, factor_vec))
```

    ## Warning in mean.default(pull(prob1_df, factor_vec)): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

### Comments:

I can take the mean of a numerical and logical vectors, but not the
character or factor vectors.

## Here we are introducing coercion by converting the vectors using the as.numeric command

``` r
as.numeric(pull(prob1_df, samp))
```

    ##  [1] -0.49043167  0.43448447 -0.02654631 -0.17513087 -0.41133838  2.52394916
    ##  [7] -0.20169637 -0.03261798 -1.48371480  0.27939178

``` r
as.numeric(pull(prob1_df, samp_gt_0))
```

    ##  [1] 0 1 0 0 0 1 0 0 0 1

``` r
as.numeric(pull(prob1_df, char_vec))
```

    ## Warning: NAs introduced by coercion

    ##  [1] NA NA NA NA NA NA NA NA NA NA

``` r
as.numeric(pull(prob1_df, factor_vec))
```

    ##  [1] 2 2 2 2 3 3 3 1 1 1

### Comments

Here we can see no change to the numeric vector and the logical vector
reassigned 0s and 1s to define the true and false values. We were not
able to reclassify the character vector to a numeric value. However, the
factor vector was reassigned to 1, 2, and 3. Interesting that it started
with 2, and not 1?

## Here we performing mathematical operations on the vectors.

``` r
as.numeric(pull(prob1_df, samp_gt_0)) * pull(prob1_df, samp)
```

    ##  [1] 0.0000000 0.4344845 0.0000000 0.0000000 0.0000000 2.5239492 0.0000000
    ##  [8] 0.0000000 0.0000000 0.2793918

``` r
as.factor(pull(prob1_df, samp_gt_0)) * pull(prob1_df, samp)
```

    ## Warning in Ops.factor(as.factor(pull(prob1_df, samp_gt_0)), pull(prob1_df, : '*'
    ## not meaningful for factors

    ##  [1] NA NA NA NA NA NA NA NA NA NA

``` r
as.numeric(as.factor(pull(prob1_df, samp_gt_0)) * pull(prob1_df, samp))
```

    ## Warning in Ops.factor(as.factor(pull(prob1_df, samp_gt_0)), pull(prob1_df, : '*'
    ## not meaningful for factors

    ##  [1] NA NA NA NA NA NA NA NA NA NA

# Problem 2
