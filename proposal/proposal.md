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
not be a fully comprehensive analysis until those can updated. Although
most effects from the transfer won’t be visible yet, many systems are
being fully transitioned into electric heating that is being funded by a
newly constructed solar panel array outside of Bangor for green
renewable energy. This means that the fossil fuel requirements will be
reduced to zero for buildings that have undergone heat-pump
installations or insulation. We will work with the price requirements of
fuel for multiple years of on campus buildings, as well as the price of
heat pump and insulation installations. Using this, we plan to show a
basic analysis on the saved fuel costs when compared to the overall
price of the transition.

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

## 3. Ethics review

<https://docs.google.com/spreadsheets/d/17HQLm0ieg3CpGigJwEUrePDcWNnYUJZW/edit#gid=570530532>

## 3. Ethics review

The biases that could effect our data visualizations and how the data
was collected could be believing that the school has completely
transformed their heating systems to electric from fossil fuels. We are
aware that that is not the case. We are also aware that the fueled
heaters were on for a part of the year that the school was not intending
for. This is not able to be seen in the data because the fuel tanks are
no longer receiving fuel refills. We also did not collect the data
ourselves. This data was collected by David Gibson and others. We do not
need to worry about misrepresentation or misleading information when it
comes to people, there would be no negative effects on people. However,
creating incorrect data visualizations and interpretations would be
confusing.

## 4. Data analysis plan

We will use variables such as gallons, we can calculate emissions,
dates/time in years to see the difference overtime, we also plan on
touching on pricing and how much money the school has saved over time.
We will talk to David about which buildings he recommends us to study.
Initially we will focus on the buildings on campus and seek advice from
David. We plan on making a bar plots to visualize and analyze which
buildings use the most fuel, and see how their fuel needs associated
prices have changed overtime. We believe we will see the most effect
from heat pump and insulation installation at Witchcliff, Seafox, Davis,
and Blair-Tyson. We will use line graphs to show their fuel uses over
long periods of time. Using a Violin graph, we hope to see if we can
tell any effects of heat pump or insulation directly, and the differing
effects of seasons on each building. Animations may also be able to show
this change effectively due to the many years of data available. For
finer analysis we can also facet wrap graphs side by side. On top of
this, we will analyze the effectiveness of different types of fuel, and
if there is any visible differences according to total gallons used and
amount of deliveries needed. We will use variables such as gallons, we
can calculate emissions, dates/time in years to see the difference
overtime, we also plan on touching on pricing and how much money the
school has saved over time. We will talk to David about which buildings
he recommends us to study. Turrets and Blair Tyson. Going forward
Seafox, Davis. Initially we will focus on the buildings on campus and
seek advice from David.

Summary Statistics:

``` r
ggplot(data = energy_use) +
geom_bar( mapping = aes(x = Building, fill = `Fuel Type` )) +
  coord_flip()
```

![](proposal_files/figure-gfm/Initial%20analysis%20graph-1.png)<!-- -->

``` r
energy_use %>%
  group_by(Building) %>%
  summarize(total_gallons = sum(Gallons, na.rm = FALSE)) %>% 
arrange(desc(total_gallons))
```

    ## # A tibble: 28 × 2
    ##    Building           total_gallons
    ##    <chr>                      <dbl>
    ##  1 Arts & Sci + Gates       144394.
    ##  2 Kaelber                  103610.
    ##  3 Blair Tyson               73379.
    ##  4 Dorr NHM                  40871.
    ##  5 Seafox                    38715.
    ##  6 Davis Center              31814.
    ##  7 Davis Village             27151.
    ##  8 Turrets                   25805.
    ##  9 Turrets Annex             20089 
    ## 10 Witchcliff                12952.
    ## # ℹ 18 more rows

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

``` r
energy_use %>%
  filter(between(`Delivery Date`, as.Date('2022-01-01'), as.Date('2023-01-01'))) 
```

    ## # A tibble: 221 × 10
    ##    `Delivery Date`     `Fuel Type`   `Tank number` Building  Gallons `Unit Cost`
    ##    <dttm>              <chr>         <chr>         <chr>       <dbl>       <dbl>
    ##  1 2022-01-06 00:00:00 DYEDKEROSENE  Tank26        Witchcli…    62.2        3.26
    ##  2 2022-01-06 00:00:00 DYEDKEROSENE  Tank27        Witchcli…   125.         3.26
    ##  3 2022-01-06 00:00:00 LIQUIDPROPANE Tank37        Turrets …   232.         1.80
    ##  4 2022-01-06 00:00:00 LIQUIDPROPANE Tank8         Arts & S…   583.         1.80
    ##  5 2022-01-07 00:00:00 LIQUIDPROPANE Tank31        Davis Vi…    89.1        1.79
    ##  6 2022-01-07 00:00:00 #2HEATINGOIL  Tank33        PRF         179.         2.94
    ##  7 2022-01-07 00:00:00 LIQUIDPROPANE Tank35        B&G          21.1        1.79
    ##  8 2022-01-08 00:00:00 #2HEATINGOIL  Tank24        Dorr NHM     47.7        2.85
    ##  9 2022-01-12 00:00:00 LIQUIDPROPANE Tank10        Hatchery     25.4        1.84
    ## 10 2022-01-13 00:00:00 #2HEATINGOIL  Tank24        Dorr NHM    132.         2.98
    ## # ℹ 211 more rows
    ## # ℹ 4 more variables: Cost <dbl>, ...8 <lgl>, ...9 <chr>, ...10 <chr>

Repeating yearly filter to compare multiple years- animation?
