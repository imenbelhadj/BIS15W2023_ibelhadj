---
title: "Lab 6 Intro"
date: "2023-01-26"
output: 
  ioslides_presentation: 
    keep_md: yes
---



## Setup
1. Login to the lab computer (please don't use your personal computer).  
2. Navigate to github.com and login.   
2. Use GitHub desktop to clone your repository to the desktop.   
5. Copy the class repository to the desktop (https://github.com/jmledford3115/datascibiol).  
6. Copy the files for today's lab from the class repository and paste them into **your** repository.  
7. Open today's lab in RStudio.  

## Review from last time
### *With a partner, discuss the following questions*
1. What is a pipe? Why are they useful in R?
2. What is the shortcut for making a pipe?
3. What is the difference between `select`, `filter`, and `mutate`?
4. What are the logistics of midterm 1?

### Warm-up
1. Open the data `ecs21351-sup-0003-SupplementS1.csv`

```
## New names:
## Rows: 571 Columns: 21
## ── Column specification
## ──────────────────────────────────────────────────────── Delimiter: "," chr
## (21): Table S3. Ecological and life history traits for the 551 species i...
## ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
## Specify the column types or set `show_col_types = FALSE` to quiet this message.
## • `` -> `...2`
## • `` -> `...3`
## • `` -> `...4`
## • `` -> `...5`
## • `` -> `...6`
## • `` -> `...7`
## • `` -> `...8`
## • `` -> `...9`
## • `` -> `...10`
## • `` -> `...11`
## • `` -> `...12`
## • `` -> `...13`
## • `` -> `...14`
## • `` -> `...15`
## • `` -> `...16`
## • `` -> `...17`
## • `` -> `...18`
## • `` -> `...19`
## • `` -> `...20`
## • `` -> `...21`
```

```
## # A tibble: 571 × 21
##    Table S3.…¹ ...2  ...3  ...4  ...5  ...6  ...7  ...8  ...9  ...10 ...11 ...12
##    <chr>       <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr>
##  1 <NA>        <NA>  <NA>  <NA>  <NA>  <NA>  <NA>  <NA>  <NA>  <NA>  <NA>  <NA> 
##  2 Order       Fami… Comm… Scie… Diet  Life… Habi… Urba… Migr… log1… Mean… Mean…
##  3 Anseriform… Anat… Amer… Anas… Vege… Long  Wetl… No    Short 3.09  9     1    
##  4 Anseriform… Anat… Amer… Anas… Vege… Midd… Wetl… No    Short 2.88  7.5   1    
##  5 Anseriform… Anat… Barr… Buce… Inve… Midd… Wetl… No    Mode… 2.96  10.5  3    
##  6 Anseriform… Anat… Blac… Bran… Vege… Long  Wetl… No    Mode… 3.11  3.5   2.5  
##  7 Anseriform… Anat… Blac… Mela… Inve… Midd… Wetl… No    Mode… 3.02  9.5   2    
##  8 Anseriform… Anat… Blac… Dend… Vege… Short Wetl… No    With… 2.88  13.5  1    
##  9 Anseriform… Anat… Blue… Anas… Vege… Midd… Wetl… No    Mode… 2.56  10    0.6  
## 10 Anseriform… Anat… Buff… Buce… Inve… Midd… Wetl… No    Short 2.60  8.5   2    
## # … with 561 more rows, 9 more variables: ...13 <chr>, ...14 <chr>,
## #   ...15 <chr>, ...16 <chr>, ...17 <chr>, ...18 <chr>, ...19 <chr>,
## #   ...20 <chr>, ...21 <chr>, and abbreviated variable name
## #   ¹​`Table S3. Ecological and life history traits for the 551 species include in the CBC trend analyses.`
```

2. Clean the names of the variables


3. Explore the data using a function of your choice
4. Are there more veggie, omni, insecivore, or nectar feeders in the data?
5. Which families are Veggie?
