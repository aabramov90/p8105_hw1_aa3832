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

``` r
library(palmerpenguins)
```

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

    ## [1] 0.07038003

``` r
mean(pull(prob1_df, samp_gt_0))
```

    ## [1] 0.6

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

    ##  [1] -0.85781416  0.34361716  0.20213293 -1.21425030  0.95073735 -0.41086717
    ##  [7]  0.46302929  1.28543730  0.02115288 -0.07937501

``` r
as.numeric(pull(prob1_df, samp_gt_0))
```

    ##  [1] 0 1 1 0 1 0 1 1 1 0

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

Here we can see no change to the numeric vector, while the logical
vector reassigned 0s and 1s to define the true and false values. We were
not able to reclassify the character vector to a numeric value. However,
the factor vector was reassigned to 1, 2, and 3. Interesting that it
started with 2, and not 1?

## Here we performing mathematical operations on the vectors.

``` r
as.numeric(pull(prob1_df, samp_gt_0)) * pull(prob1_df, samp)
```

    ##  [1] 0.00000000 0.34361716 0.20213293 0.00000000 0.95073735 0.00000000
    ##  [7] 0.46302929 1.28543730 0.02115288 0.00000000

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

Here is a quick snapshot of the penguins dataset featuring the first ten
rows and columns.

``` r
data("penguins", package = "palmerpenguins")
head(penguins, n=10)
```

    ## # A tibble: 10 x 8
    ##    species island bill_length_mm bill_depth_mm flipper_length_… body_mass_g
    ##    <fct>   <fct>           <dbl>         <dbl>            <int>       <int>
    ##  1 Adelie  Torge…           39.1          18.7              181        3750
    ##  2 Adelie  Torge…           39.5          17.4              186        3800
    ##  3 Adelie  Torge…           40.3          18                195        3250
    ##  4 Adelie  Torge…           NA            NA                 NA          NA
    ##  5 Adelie  Torge…           36.7          19.3              193        3450
    ##  6 Adelie  Torge…           39.3          20.6              190        3650
    ##  7 Adelie  Torge…           38.9          17.8              181        3625
    ##  8 Adelie  Torge…           39.2          19.6              195        4675
    ##  9 Adelie  Torge…           34.1          18.1              193        3475
    ## 10 Adelie  Torge…           42            20.2              190        4250
    ## # … with 2 more variables: sex <fct>, year <int>

The penguins dataset has these variables:

``` r
names(penguins)
```

    ## [1] "species"           "island"            "bill_length_mm"   
    ## [4] "bill_depth_mm"     "flipper_length_mm" "body_mass_g"      
    ## [7] "sex"               "year"

The penguins dataset has this many rows and columns.

``` r
nrow(penguins)
```

    ## [1] 344

``` r
ncol(penguins)
```

    ## [1] 8
