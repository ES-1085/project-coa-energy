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
school uses due to the newly installed insulation system. This will be
found by calculating how much less oil the school is using, we will be
able to calculate how much the school has decreased their CO2 emission.
This data was collected by David Gibson. The data was collected through
the yearly energy center analysis. This is a long term goal which is to
make COA fossil free, net 0, by 2030. Through this project we hope to
evaluate whether or not the school is on track to meet that goal when it
comes to energy use of buildings. Our variables include the date the
fuel was purchased, the cost, the amount of fuel in gallons. The
buildings we will focus on will be Turrets and Blair-Tyson, as well as
Seafox and Davis and other on campus locations with the proper data. The
dataset is not fully up to date with the effects of new heat system
installations, nor will they be until the end of the year so this will
not be a fully comprehensive analysis until those can updated.

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
glimpse(energy_use)
```

    ## Rows: 2,700
    ## Columns: 10
    ## $ `Delivery Date` <dttm> 2014-01-03, 2014-01-03, 2014-01-04, 2014-01-04, 2014-…
    ## $ `Fuel Type`     <chr> "LIQUIDPROPANE", "DYEDKEROSENE", "#2HEATINGOIL", "#2HE…
    ## $ `Tank number`   <chr> "Tank14", "Tank27", "Tank24", "Tank3", "Tank5", "Tank1…
    ## $ Building        <chr> "171 Beech Hill Road", "Witchcliff Apartments", "Dorr …
    ## $ Gallons         <dbl> 10.0, 170.0, 185.3, 264.9, 281.4, 299.1, 40.9, 71.6, 8…
    ## $ `Unit Cost`     <dbl> 1.8481, 3.7304, 3.3417, 3.3417, 3.3417, 3.2998, 1.8481…
    ## $ Cost            <dbl> 18.48, 634.17, 619.22, 885.22, 940.35, 986.97, 75.59, …
    ## $ ...8            <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
    ## $ ...9            <chr> "Tank 1", NA, "Tank 3", "Tank 4", "Tank 5", NA, "Tank …
    ## $ ...10           <chr> "Peach House", NA, "Seafox", "Cottage", "Turrets", NA,…

<https://docs.google.com/spreadsheets/d/17HQLm0ieg3CpGigJwEUrePDcWNnYUJZW/edit#gid=570530532>

## 3. Ethics review

## 4. Data analysis plan

We will use variables such as gallons, we can calculate emissions,
dates/time in years to see the difference overtime, we also plan on
touching on pricing and how much money the school has saved over time.
We will talk to David about which buildings he recommends us to study.
Initially we will focus on the buildings on campus and seek advice from
David.

``` r
ggplot(data = energy_use) +
geom_bar( mapping = aes(x = Building, fill = `Fuel Type` )) +
  coord_flip()
```

![](proposal_files/figure-gfm/Initial%20analysis%20graph-1.png)<!-- -->

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
