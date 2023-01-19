---
title: "Lab 3 Homework"
author: "Imen Belhadj"
date: "2023-01-18"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library("tidyverse")
```

## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

```r
#The data is taken from the Excel file titled, mammals_sleep_allison_cicchetti_1976.
getwd()
```

```
## [1] "C:/Users/imenb/OneDrive/Desktop/BIS15W2023_ibelhadj/lab3"
```

```r
sleep <-readr::read_csv("data/mammals_sleep_allison_cicchetti_1976.csv")
```

```
## Rows: 62 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): species
## dbl (10): body weight in kg, brain weight in g, slow wave ("nondreaming") sl...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

2. Store these data into a new data frame `sleep`.

```r
msleep <- sleep
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

```r
dim(msleep)
```

```
## [1] 62 11
```

```r
#Sleep data is 62 rows by 11 columns.
```

4. Are there any NAs in the data? How did you determine this? Please show your code.  

```r
#There are no NAs in the data because the summary function shows the statistical values of each column without any errors. 
summary(msleep)
```

```
##    species          body weight in kg  brain weight in g
##  Length:62          Min.   :   0.005   Min.   :   0.14  
##  Class :character   1st Qu.:   0.600   1st Qu.:   4.25  
##  Mode  :character   Median :   3.342   Median :  17.25  
##                     Mean   : 198.790   Mean   : 283.13  
##                     3rd Qu.:  48.202   3rd Qu.: 166.00  
##                     Max.   :6654.000   Max.   :5712.00  
##  slow wave ("nondreaming") sleep (hrs/day)
##  Min.   :-999.000                         
##  1st Qu.:   2.375                         
##  Median :   7.400                         
##  Mean   :-218.866                         
##  3rd Qu.:  10.550                         
##  Max.   :  17.900                         
##  paradoxical ("dreaming") sleep (hrs/day)
##  Min.   :-999.000                        
##  1st Qu.:   0.500                        
##  Median :   1.300                        
##  Mean   :-191.764                        
##  3rd Qu.:   2.275                        
##  Max.   :   6.600                        
##  total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)
##  Min.   :-999.00                                                
##  1st Qu.:   6.20                                                
##  Median :  10.30                                                
##  Mean   : -54.60                                                
##  3rd Qu.:  13.15                                                
##  Max.   :  19.90                                                
##  maximum life span (years) gestation time (days) predation index (1-5)
##  Min.   :-999.00           Min.   :-999.00       Min.   :1.000        
##  1st Qu.:   5.25           1st Qu.:  30.25       1st Qu.:2.000        
##  Median :  13.35           Median :  63.00       Median :3.000        
##  Mean   : -45.86           Mean   :  68.72       Mean   :2.871        
##  3rd Qu.:  27.00           3rd Qu.: 195.00       3rd Qu.:4.000        
##  Max.   : 100.00           Max.   : 645.00       Max.   :5.000        
##  sleep exposure index (1-5) overall danger index (1-5)
##  Min.   :1.000              Min.   :1.000             
##  1st Qu.:1.000              1st Qu.:1.000             
##  Median :2.000              Median :2.000             
##  Mean   :2.419              Mean   :2.613             
##  3rd Qu.:4.000              3rd Qu.:4.000             
##  Max.   :5.000              Max.   :5.000
```
5. Show a list of the column names is this data frame.

```r
colnames(msleep)
```

```
##  [1] "species"                                                        
##  [2] "body weight in kg"                                              
##  [3] "brain weight in g"                                              
##  [4] "slow wave (\"nondreaming\") sleep (hrs/day)"                    
##  [5] "paradoxical (\"dreaming\") sleep (hrs/day)"                     
##  [6] "total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)"
##  [7] "maximum life span (years)"                                      
##  [8] "gestation time (days)"                                          
##  [9] "predation index (1-5)"                                          
## [10] "sleep exposure index (1-5)"                                     
## [11] "overall danger index (1-5)"
```
6. How many herbivores are represented in the data?  

```r
table(msleep$`predation index (1-5)`)
```

```
## 
##  1  2  3  4  5 
## 14 15 12  7 14
```

```r
#There are 14 herbivores represented in the data (14 mammals with a predation index of 5).
```
7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
small_mammals <- subset(msleep, `body weight in kg`<=1)
large_mammals <- subset(msleep, `body weight in kg`>=200)
```


8. What is the mean weight for both the small and large mammals?

```r
colMeans(small_mammals [,2])
```

```
## body weight in kg 
##         0.3324286
```

```r
colMeans(large_mammals[,2])
```

```
## body weight in kg 
##          1596.143
```
9. Using a similar approach as above, do large or small animals sleep longer on average?  

```r
colMeans(small_mammals[,6])
```

```
## total sleep (hrs/day)  (sum of slow wave and paradoxical sleep) 
##                                                        12.71905
```


```r
colMeans(large_mammals[,6])
```

```
## total sleep (hrs/day)  (sum of slow wave and paradoxical sleep) 
##                                                       -281.7143
```

```r
#Because there are big outliers in the large_mammal subset, the true average of total sleep per day for the large mammals cannot be determined without excluding the outlier(s).
```

10. Which animal is the sleepiest among the entire dataframe?

```r
max(msleep$`total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)`)
```

```
## [1] 19.9
```


```r
which(msleep$`total sleep (hrs/day)  (sum of slow wave and paradoxical sleep)`==19.9)
```

```
## [1] 33
```

```r
#The little brown rat (#33) in the entire dataframe is the sleepiest animal. 
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
