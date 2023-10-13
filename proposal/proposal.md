Project proposal
================
COA Energy, Sierra, Hunter, Laila

``` r
library(tidyverse)
library(broom)
```

## 1. Introduction

We plan on analyzing and interpreting the energy data set to make an
assessment on how many gallons of fuel the school has used over a span
of 9-10 years. We are curious about learning how much less emissions the
school uses from the newly installed insulation system. This will be
found by calculating how much less oil the school is using, we will be
able to calculate how much the school has decreased their CO2 emission.
This data was collected by David Gibson. The data was collected through
the yearly energy center analysis (we will edit this for accuracy). This
is a long term goal which is to make COA fossil free, net 0, by 2030.
Through this project we hope to evaluate whether or not the school is on
track to meet that goal when it comes to energy use of buildings. Our
variables include the data the fuel was purchased, the cost, the amount
of fuel in gallons, (after we talk with David Gibson we will update this
document to address which specific buildings or areas we would like to
focus on.)

## 2. Data

``` r
library(readxl)
energy_use <- read_excel("../data/energy_use.xlsx")
```

    ## New names:
    ## • `` -> `...8`
    ## • `` -> `...9`
    ## • `` -> `...10`

``` r
# View(energy_use)
```

## 3. Ethics review

## 4. Data analysis plan

We will use variables such as gallons, we can calculate emissions,
dates/time in years to see the difference overtime, we also plan on
touching on pricing and how much money the school has saved over time.
We will talk to David about which buildings he recommends us to study.
Initially we will focus on the buildings on campus and seek advice from
David.

``` r
energy_use %>%
count(Building, Gallons)
```

    ## # A tibble: 2,542 × 3
    ##    Building            Gallons     n
    ##    <chr>                 <dbl> <int>
    ##  1 171 Beech Hill Road   -25.5     1
    ##  2 171 Beech Hill Road     1.8     1
    ##  3 171 Beech Hill Road     8       1
    ##  4 171 Beech Hill Road    10       1
    ##  5 171 Beech Hill Road    11.2     1
    ##  6 171 Beech Hill Road    13.4     1
    ##  7 171 Beech Hill Road    14.4     1
    ##  8 171 Beech Hill Road    14.8     1
    ##  9 171 Beech Hill Road    15       1
    ## 10 171 Beech Hill Road    15.3     1
    ## # ℹ 2,532 more rows
