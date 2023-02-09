---
title: "Lab 9 Intro"
date: "2023-02-09"
output: 
  ioslides_presentation: 
    keep_md: yes
---



## Seating
1. If you already have a group, it will be helpful to start sitting next to each other.
2. If you don't have a group, hang tight we are working on it.
3. Please setup your computer as normal for today.

## Warm-up
1. In the data folder there is an epidemiology data set on an outbreak of malaria.

```
## Rows: 3038 Columns: 10
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (3): location_name, Province, District
## dbl  (5): malaria_rdt_0-4, malaria_rdt_5-14, malaria_rdt_15, malaria_tot, newid
## date (2): data_date, submitted_date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## # A tibble: 3,038 × 10
##    locat…¹ data_date  submitte…² provi…³ distr…⁴ malar…⁵ malar…⁶ malar…⁷ malar…⁸
##    <chr>   <date>     <date>     <chr>   <chr>     <dbl>   <dbl>   <dbl>   <dbl>
##  1 Facili… 2020-08-11 2020-08-12 North   Spring       11      12      23      46
##  2 Facili… 2020-08-11 2020-08-12 North   Bolo         11      10       5      26
##  3 Facili… 2020-08-11 2020-08-12 North   Dingo         8       5       5      18
##  4 Facili… 2020-08-11 2020-08-12 North   Bolo         16      16      17      49
##  5 Facili… 2020-08-11 2020-08-12 North   Bolo          9       2       6      17
##  6 Facili… 2020-08-11 2020-08-12 North   Dingo         3       1       4       8
##  7 Facili… 2020-08-10 2020-08-12 North   Dingo         4       0       3       7
##  8 Facili… 2020-08-10 2020-08-12 North   Bolo         15      14      13      42
##  9 Facili… 2020-08-09 2020-08-12 North   Bolo         11      11      13      35
## 10 Facili… 2020-08-08 2020-08-12 North   Bolo         19      15      15      49
## # … with 3,028 more rows, 1 more variable: newid <dbl>, and abbreviated
## #   variable names ¹​location_name, ²​submitted_date, ³​province, ⁴​district,
## #   ⁵​malaria_rdt_0_4, ⁶​malaria_rdt_5_14, ⁷​malaria_rdt_15, ⁸​malaria_tot
```

2. `rdt` refers to rapid diagnostic test and they are identified here by age group.

3. Make the data tidy and store them as a new object.

```
## # A tibble: 9,114 × 8
##    location_name data_date  submitted_date province district newid age_c…¹ cases
##    <chr>         <date>     <date>         <chr>    <chr>    <dbl> <chr>   <dbl>
##  1 Facility 1    2020-08-11 2020-08-12     North    Spring       1 malari…    11
##  2 Facility 1    2020-08-11 2020-08-12     North    Spring       1 malari…    12
##  3 Facility 1    2020-08-11 2020-08-12     North    Spring       1 malari…    23
##  4 Facility 2    2020-08-11 2020-08-12     North    Bolo         2 malari…    11
##  5 Facility 2    2020-08-11 2020-08-12     North    Bolo         2 malari…    10
##  6 Facility 2    2020-08-11 2020-08-12     North    Bolo         2 malari…     5
##  7 Facility 3    2020-08-11 2020-08-12     North    Dingo        3 malari…     8
##  8 Facility 3    2020-08-11 2020-08-12     North    Dingo        3 malari…     5
##  9 Facility 3    2020-08-11 2020-08-12     North    Dingo        3 malari…     5
## 10 Facility 4    2020-08-11 2020-08-12     North    Bolo         4 malari…    16
## # … with 9,104 more rows, and abbreviated variable name ¹​age_class
```



4. Which district had the highest *total* number of cases on July 30, 2020?

```
## # A tibble: 1 × 2
##   district total_cases
##   <chr>          <dbl>
## 1 Bolo             347
```


