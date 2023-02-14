---
title: "Lab 10 Intro"
date: "2023-02-14"
output: 
  ioslides_presentation: 
    keep_md: yes
---



## Seating & Set-up
1. Please make sure that you sit next to your group members for the rest of the quarter.
2. Please set-up your computer as normal.

## Warm-up
1. Please load the homerange data `Tamburelloetal_HomeRangeDatabase.csv`
2. Show the min, mean, and max log10.mass by taxonomic class in the dataset.
3. Make a plot that best summarizes this output.


```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```
## # A tibble: 4 × 4
##   class          min_mass mean_mass max_mass
##   <chr>             <dbl>     <dbl>    <dbl>
## 1 actinopterygii   -0.658      2.00     3.55
## 2 aves              0.712      1.99     4.95
## 3 mammalia          0.620      3.25     6.60
## 4 reptilia          0.539      2.53     4.03
```



