---
title: "Midterm 1"
author: "Imen Belhadj"
date: "2023-01-31"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. You may use any resources to answer these questions (including each other), but you may not post questions to Open Stacks or external help sites. There are 15 total questions, each is worth 2 points.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse
If you plan to use any other libraries to complete this assignment then you should load them here.

```r
library("tidyverse")
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
library("janitor")
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

## Questions  

Wikipedia's definition of [data science](https://en.wikipedia.org/wiki/Data_science): "Data science is an interdisciplinary field that uses scientific methods, processes, algorithms and systems to extract knowledge and insights from noisy, structured and unstructured data, and apply knowledge and actionable insights from data across a broad range of application domains."  

1. (2 points) Consider the definition of data science above. Although we are only part-way through the quarter, what specific elements of data science do you feel we have practiced? Provide at least one specific example.  
#We have practiced removing unwanted values(such the -999 that represent NAs) that skew statistical calculations.  

2. (2 points) What is the most helpful or interesting thing you have learned so far in BIS 15L? What is something that you think needs more work or practice?  


In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ElephantsMF`. These data are from Phyllis Lee, Stirling University, and are related to Lee, P., et al. (2013), "Enduring consequences of early experiences: 40-year effects on survival and success among African elephants (Loxodonta africana)," Biology Letters, 9: 20130011. [kaggle](https://www.kaggle.com/mostafaelseidy/elephantsmf).  

3. (2 points) Please load these data as a new object called `elephants`. Use the function(s) of your choice to get an idea of the structure of the data. Be sure to show the class of each variable.

```r
elephants<-readr::read_csv("data/ElephantsMF.csv")
```

```
## Rows: 288 Columns: 3
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (1): Sex
## dbl (2): Age, Height
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


4. (2 points) Change the names of the variables to lower case and change the class of the variable `sex` to a factor.

```r
elephants<-janitor::clean_names(elephants)
glimpse(elephants)
```

```
## Rows: 288
## Columns: 3
## $ age    <dbl> 1.40, 17.50, 12.75, 11.17, 12.67, 12.67, 12.25, 12.17, 28.17, 1…
## $ height <dbl> 120.00, 227.00, 235.00, 210.00, 220.00, 189.00, 225.00, 204.00,…
## $ sex    <chr> "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M", "M"…
```

```r
elephants %>% mutate_if(is.character,as.factor)
```

```
## # A tibble: 288 × 3
##      age height sex  
##    <dbl>  <dbl> <fct>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # … with 278 more rows
```

```r
#OR elephants$sex <- as.factor(elephants$sex)
elephants
```

```
## # A tibble: 288 × 3
##      age height sex  
##    <dbl>  <dbl> <chr>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # … with 278 more rows
```

5. (2 points) How many male and female elephants are represented in the data? #OR elephants %>% count(sex)

```r
melephants<-elephants %>% 
  filter(sex=="M")
count(melephants)
```

```
## # A tibble: 1 × 1
##       n
##   <int>
## 1   138
```


```r
felephants<-elephants %>% 
  filter(sex=="F")
count(felephants)
```

```
## # A tibble: 1 × 1
##       n
##   <int>
## 1   150
```

```r
elephants %>% 
  count(sex)
```

```
## # A tibble: 2 × 2
##   sex       n
##   <chr> <int>
## 1 F       150
## 2 M       138
```

6. (2 points) What is the average age of all elephants in the data?

```r
mean(elephants$age)
```

```
## [1] 10.97132
```

```r
#OR elephants %>%  summarize(mean_age=mean(age))
```

7. (2 points) How does the average age and height of elephants compare by sex?

```r
elephants %>% 
  group_by(sex) %>% 
  summarise(mean_age=mean(age),
            mean_height=mean(height))
```

```
## # A tibble: 2 × 3
##   sex   mean_age mean_height
##   <chr>    <dbl>       <dbl>
## 1 F        12.8         190.
## 2 M         8.95        185.
```

```r
mean(felephants$height)
```

```
## [1] 190.0307
```

```r
#Female elephants have a larger average height than male elephants.
```
8. (2 points) How does the average height of elephants compare by sex for individuals over 20 years old. Include the min and max height as well as the number of individuals in the sample as part of your analysis.  

```r
elephants %>% 
  filter(age>20) %>% 
  group_by(sex) %>% 
  summarise(min_height=min(height),
            max_height=max(height),
            mean_height=mean(height),
            n_elephants=n())
```

```
## # A tibble: 2 × 5
##   sex   min_height max_height mean_height n_elephants
##   <chr>      <dbl>      <dbl>       <dbl>       <int>
## 1 F           193.       278.        232.          37
## 2 M           229.       304.        270.          13
```





For the next series of questions, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.  

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the midterm 1 folder.  

9. (2 points) Load `IvindoData_DryadVersion.csv` and use the function(s) of your choice to get an idea of the overall structure. Change the variables `HuntCat` and `LandUse` to factors.

```r
vertebrates<-readr::read_csv("data/IvindoData_DryadVersion.csv")
```

```
## Rows: 24 Columns: 26
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (2): HuntCat, LandUse
## dbl (24): TransectID, Distance, NumHouseholds, Veg_Rich, Veg_Stems, Veg_lian...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
vertebrates %>% mutate_if(is.character,as.factor)
```

```
## # A tibble: 24 × 26
##    TransectID Distance HuntCat  NumHou…¹ LandUse Veg_R…² Veg_S…³ Veg_l…⁴ Veg_DBH
##         <dbl>    <dbl> <fct>       <dbl> <fct>     <dbl>   <dbl>   <dbl>   <dbl>
##  1          1     7.14 Moderate       54 Park       16.7    31.2    5.78    49.6
##  2          2    17.3  None           54 Park       15.8    37.4   13.2     34.6
##  3          2    18.3  None           29 Park       16.9    32.3    4.75    42.8
##  4          3    20.8  None           29 Logging    12.4    29.4    9.78    36.6
##  5          4    16.0  None           29 Park       17.1    36     13.2     41.5
##  6          5    17.5  None           29 Park       16.5    29.2   12.9     44.1
##  7          6    24.1  None           29 Park       14.8    31.2    8.38    51.2
##  8          7    19.8  None           54 Logging    13.2    32.6    8.38    41.9
##  9          8     5.78 High           25 Neither    12.6    23.7    5.13    45.2
## 10          9     5.13 High           73 Logging    16      27.1    9.75    69.3
## # … with 14 more rows, 17 more variables: Veg_Canopy <dbl>,
## #   Veg_Understory <dbl>, RA_Apes <dbl>, RA_Birds <dbl>, RA_Elephant <dbl>,
## #   RA_Monkeys <dbl>, RA_Rodent <dbl>, RA_Ungulate <dbl>,
## #   Rich_AllSpecies <dbl>, Evenness_AllSpecies <dbl>,
## #   Diversity_AllSpecies <dbl>, Rich_BirdSpecies <dbl>,
## #   Evenness_BirdSpecies <dbl>, Diversity_BirdSpecies <dbl>,
## #   Rich_MammalSpecies <dbl>, Evenness_MammalSpecies <dbl>, …
```

10. (4 points) For the transects with high and moderate hunting intensity, how does the average diversity of birds and mammals compare?

```r
vertebrates %>% 
  filter(HuntCat=="High") %>% 
  summarise(mean_bird_diversity=mean(Diversity_BirdSpecies),
            mean_mammal_diversity=mean(Diversity_MammalSpecies),
            nsamples=n())
```

```
## # A tibble: 1 × 3
##   mean_bird_diversity mean_mammal_diversity nsamples
##                 <dbl>                 <dbl>    <int>
## 1                1.66                  1.74        7
```


```r
vertebrates %>% 
  filter(HuntCat=="Moderate") %>% 
  summarise(mean_bird_diversity=mean(Diversity_BirdSpecies),
            mean_mammal_diversity=mean(Diversity_MammalSpecies),
            nsamples=n())
```

```
## # A tibble: 1 × 3
##   mean_bird_diversity mean_mammal_diversity nsamples
##                 <dbl>                 <dbl>    <int>
## 1                1.62                  1.68        8
```


```r
mean(vertebrates$Diversity_MammalSpecies)
```

```
## [1] 1.697875
```

```r
names(vertebrates)
```

```
##  [1] "TransectID"              "Distance"               
##  [3] "HuntCat"                 "NumHouseholds"          
##  [5] "LandUse"                 "Veg_Rich"               
##  [7] "Veg_Stems"               "Veg_liana"              
##  [9] "Veg_DBH"                 "Veg_Canopy"             
## [11] "Veg_Understory"          "RA_Apes"                
## [13] "RA_Birds"                "RA_Elephant"            
## [15] "RA_Monkeys"              "RA_Rodent"              
## [17] "RA_Ungulate"             "Rich_AllSpecies"        
## [19] "Evenness_AllSpecies"     "Diversity_AllSpecies"   
## [21] "Rich_BirdSpecies"        "Evenness_BirdSpecies"   
## [23] "Diversity_BirdSpecies"   "Rich_MammalSpecies"     
## [25] "Evenness_MammalSpecies"  "Diversity_MammalSpecies"
```

11. (4 points) One of the conclusions in the study is that the relative abundance of animals drops off the closer you get to a village. Let's try to reconstruct this (without the statistics). How does the relative abundance (RA) of apes, birds, elephants, monkeys, rodents, and ungulates compare between sites that are less than 3km from a village to sites that are greater than 25km from a village? The variable `Distance` measures the distance of the transect from the nearest village. Hint: try using the `across` operator.  

```r
vertebrates %>% 
  filter(Distance>3 & Distance<25) %>% 
  summarise(across(c(RA_Apes,RA_Birds,RA_Elephant,RA_Monkeys,RA_Rodent,RA_Ungulate), 
                   mean, na.rm=T))
```

```
## # A tibble: 1 × 6
##   RA_Apes RA_Birds RA_Elephant RA_Monkeys RA_Rodent RA_Ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    2.09     58.2       0.609       31.5      3.31        4.20
```

```r
#OR vertebrates %>% 
 #filter(Distance<3) %>% 
  #summarize(across(contains("RA_"), mean))

#OR vertebrates %>% 
  #filter(Distance>25) %>% 
  #summarize(across(contains("RA_"), mean))
```

12. (4 points) Based on your interest, do one exploratory analysis on the `gabon` data of your choice. This analysis needs to include a minimum of two functions in `dplyr.`
#Which 'Park' transect has the highest species richness and the lowest species evenness.

```r
vertebrates %>% 
  filter(LandUse=="Park") %>% 
  summarise(across(c(Rich_AllSpecies,Evenness_AllSpecies),
                   max,na.rm=T))
```

```
## # A tibble: 1 × 2
##   Rich_AllSpecies Evenness_AllSpecies
##             <dbl>               <dbl>
## 1              24               0.818
```

```r
vertebrates %>% 
  filter(LandUse=="Park") %>% 
  select(Rich_AllSpecies,Evenness_AllSpecies) %>% 
  summarise(across(c(Rich_AllSpecies,Evenness_AllSpecies),
                   min,na.rm=T))
```

```
## # A tibble: 1 × 2
##   Rich_AllSpecies Evenness_AllSpecies
##             <dbl>               <dbl>
## 1              20                0.74
```


