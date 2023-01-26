---
title: "Penguins"
output: 
  html_document: 
    keep_md: yes
date: "2023-01-26"
---




```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.0 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```


```r
ecosphere<-readr::read_csv("data/ecs21351-sup-0003-SupplementS1.csv",skip=2)
```

```
## Rows: 569 Columns: 21
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (10): Order, Family, Common Name, Scientific Name, Diet, Life Expectancy...
## dbl (11): log10(mass), Mean Eggs per Clutch, Mean Age at Sexual Maturity, Po...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
names(ecosphere)
```

```
##  [1] "Order"                       "Family"                     
##  [3] "Common Name"                 "Scientific Name"            
##  [5] "Diet"                        "Life Expectancy"            
##  [7] "Habitat"                     "Urban Affiliate"            
##  [9] "Migratory Strategy"          "log10(mass)"                
## [11] "Mean Eggs per Clutch"        "Mean Age at Sexual Maturity"
## [13] "Population Size"             "Winter Range Area"          
## [15] "Range in CBC"                "Strata"                     
## [17] "Circles"                     "Feeder Bird"                
## [19] "Median Trend"                "Lower 95% CI"               
## [21] "Upper 95% CI"
```

```r
ecosphere<-ecosphere %>% clean_names()
names(ecosphere)
```

```
##  [1] "order"                       "family"                     
##  [3] "common_name"                 "scientific_name"            
##  [5] "diet"                        "life_expectancy"            
##  [7] "habitat"                     "urban_affiliate"            
##  [9] "migratory_strategy"          "log10_mass"                 
## [11] "mean_eggs_per_clutch"        "mean_age_at_sexual_maturity"
## [13] "population_size"             "winter_range_area"          
## [15] "range_in_cbc"                "strata"                     
## [17] "circles"                     "feeder_bird"                
## [19] "median_trend"                "lower_95_percent_ci"        
## [21] "upper_95_percent_ci"
```

```r
summary(ecosphere)
```

```
##     order              family          common_name        scientific_name   
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##      diet           life_expectancy      habitat          urban_affiliate   
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  migratory_strategy   log10_mass    mean_eggs_per_clutch
##  Length:569         Min.   :0.480   Min.   : 1.000      
##  Class :character   1st Qu.:1.365   1st Qu.: 3.000      
##  Mode  :character   Median :1.890   Median : 4.000      
##                     Mean   :2.012   Mean   : 4.527      
##                     3rd Qu.:2.685   3rd Qu.: 5.000      
##                     Max.   :4.040   Max.   :17.000      
##                     NA's   :18      NA's   :18          
##  mean_age_at_sexual_maturity population_size     winter_range_area  
##  Min.   : 0.200              Min.   :    15000   Min.   :       11  
##  1st Qu.: 1.000              1st Qu.:  1100000   1st Qu.:   819357  
##  Median : 1.000              Median :  4900000   Median :  2189639  
##  Mean   : 1.592              Mean   : 18446745   Mean   :  5051047  
##  3rd Qu.: 2.000              3rd Qu.: 18000000   3rd Qu.:  6778598  
##  Max.   :12.500              Max.   :300000000   Max.   :185968946  
##  NA's   :18                  NA's   :291         NA's   :18         
##   range_in_cbc        strata          circles       feeder_bird       
##  Min.   :  0.00   Min.   :  1.00   Min.   :   2.0   Length:569        
##  1st Qu.:  2.35   1st Qu.:  3.00   1st Qu.:  46.5   Class :character  
##  Median : 30.30   Median : 11.00   Median : 184.0   Mode  :character  
##  Mean   : 38.48   Mean   : 32.43   Mean   : 558.9                     
##  3rd Qu.: 72.95   3rd Qu.: 42.00   3rd Qu.: 661.0                     
##  Max.   :100.00   Max.   :159.00   Max.   :3202.0                     
##  NA's   :18       NA's   :18       NA's   :18                         
##   median_trend   lower_95_percent_ci upper_95_percent_ci
##  Min.   :0.739   Min.   :0.5780      Min.   :    0.798  
##  1st Qu.:0.993   1st Qu.:0.9675      1st Qu.:    1.011  
##  Median :1.009   Median :0.9930      Median :    1.027  
##  Mean   :1.016   Mean   :0.9857      Mean   :   33.709  
##  3rd Qu.:1.030   3rd Qu.:1.0140      3rd Qu.:    1.055  
##  Max.   :1.396   Max.   :1.3080      Max.   :18000.000  
##  NA's   :18      NA's   :18          NA's   :18
```

```r
ecosphere %>% 
  tabyl(diet) %>% 
  arrange(desc(n))
```

```
##           diet   n    percent valid_percent
##  Invertebrates 216 0.37961336    0.39201452
##       Omnivore 114 0.20035149    0.20689655
##    Vertebrates 102 0.17926186    0.18511797
##           Seed  64 0.11247803    0.11615245
##     Vegetation  31 0.05448155    0.05626134
##           <NA>  18 0.03163445            NA
##         Nectar  13 0.02284710    0.02359347
##          Fruit  11 0.01933216    0.01996370
```

```r
ecosphere %>% 
  filter(diet=="Vegetation") %>% 
  select(family,diet) %>% 
  tabyl(diet)
```

```
##        diet  n percent
##  Vegetation 31       1
```


