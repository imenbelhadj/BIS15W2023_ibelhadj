---
title: "Lab 5 Intro"
date: "2023-01-24"
output: 
  ioslides_presentation: 
    keep_md: yes
---



## Setup
1. Login to the lab computer (please don't use your personal computer).  
2. Navigate to github.com and login.   
2. Copy your repository to the desktop.   
5. Copy the class repository to the desktop (https://github.com/jmledford3115/datascibiol).  
6. Copy the files for today's lab from the class repository and paste them into **your** repository.  
7. Open today's lab in RStudio.  

## Review from last time
### *With a partner, discuss the following questions*
1. What are the characteristics of `tidy` data? Every cell has unique value.    
2. What is the difference between `select` and `filter`? Select is used to operate between columns, filter is for operating betwee rows.
3. When is your first midterm? January 31st

## Warm-up
1. Load the bison data.

```
## Rows: 8325 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (3): data_code, animal_code, animal_sex
## dbl (5): rec_year, rec_month, rec_day, animal_weight, animal_yob
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
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

2. What are the dimesions and structure of the data?

```
## [1] 8325    8
```

```
## Rows: 8,325
## Columns: 8
## $ data_code     <chr> "CBH01", "CBH01", "CBH01", "CBH01", "CBH01", "CBH01", "C…
## $ rec_year      <dbl> 1994, 1994, 1994, 1994, 1994, 1994, 1994, 1994, 1994, 19…
## $ rec_month     <dbl> 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, 11, …
## $ rec_day       <dbl> 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8,…
## $ animal_code   <chr> "813", "834", "B-301", "B-402", "B-403", "B-502", "B-503…
## $ animal_sex    <chr> "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "F", "…
## $ animal_weight <dbl> 890, 1074, 1060, 989, 1062, 978, 1068, 1024, 978, 1188, …
## $ animal_yob    <dbl> 1981, 1983, 1983, 1984, 1984, 1985, 1985, 1985, 1986, 19…
```

3. We are only interested in code, sex, weight, year of birth. Restrict the data to these variables and store the dataframe as a new object.

```
## [1] "data_code"     "rec_year"      "rec_month"     "rec_day"      
## [5] "animal_code"   "animal_sex"    "animal_weight" "animal_yob"
```

```
## # A tibble: 8,325 × 4
##    data_code animal_sex animal_weight animal_yob
##    <chr>     <chr>              <dbl>      <dbl>
##  1 CBH01     F                    890       1981
##  2 CBH01     F                   1074       1983
##  3 CBH01     F                   1060       1983
##  4 CBH01     F                    989       1984
##  5 CBH01     F                   1062       1984
##  6 CBH01     F                    978       1985
##  7 CBH01     F                   1068       1985
##  8 CBH01     F                   1024       1985
##  9 CBH01     F                    978       1986
## 10 CBH01     F                   1188       1986
## # … with 8,315 more rows
```

4. Pull out the animals born between 1980-1990.

```
## # A tibble: 435 × 4
##    data_code animal_sex animal_weight animal_yob
##    <chr>     <chr>              <dbl>      <dbl>
##  1 CBH01     F                    890       1981
##  2 CBH01     F                   1074       1983
##  3 CBH01     F                   1060       1983
##  4 CBH01     F                    989       1984
##  5 CBH01     F                   1062       1984
##  6 CBH01     F                    978       1985
##  7 CBH01     F                   1068       1985
##  8 CBH01     F                   1024       1985
##  9 CBH01     F                    978       1986
## 10 CBH01     F                   1188       1986
## # … with 425 more rows
```

5. How many male and female bison are represented between 1980-1990?


6. Between 1980-1990, were males or females larger on average?

```
## [1] 1017.314
```

```
## [1] 1543.333
```





