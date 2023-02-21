---
title: "Lab 11 Homework"
author: "Imen Belhadj"
date: "2023-02-20"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

**In this homework, you should make use of the aesthetics you have learned. It's OK to be flashy!**

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library("tidyverse")
library("janitor")
library("here")
library("naniar")
```

## Resources
The idea for this assignment came from [Rebecca Barter's](http://www.rebeccabarter.com/blog/2017-11-17-ggplot2_tutorial/) ggplot tutorial so if you get stuck this is a good place to have a look.  

## Gapminder
For this assignment, we are going to use the dataset [gapminder](https://cran.r-project.org/web/packages/gapminder/index.html). Gapminder includes information about economics, population, and life expectancy from countries all over the world. You will need to install it before use. This is the same data that we will use for midterm 2 so this is good practice.

```r
#install.packages("gapminder")
library("gapminder")
```

## Questions
The questions below are open-ended and have many possible solutions. Your approach should, where appropriate, include numerical summaries and visuals. Be creative; assume you are building an analysis that you would ultimately present to an audience of stakeholders. Feel free to try out different `geoms` if they more clearly present your results.  

**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine how NA's are treated in the data.** 

```r
glimpse(gapminder)
```

```
## Rows: 1,704
## Columns: 6
## $ country   <fct> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanistan", …
## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, …
## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, …
## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.8…
## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 12…
## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134, …
```


```r
dim(gapminder)
```

```
## [1] 1704    6
```

```r
view(gapminder)
naniar::any_na(gapminder)
```

```
## [1] FALSE
```

**2. Among the interesting variables in gapminder is life expectancy. How has global life expectancy changed between 1952 and 2007?**

```r
gapminder %>% 
  group_by(year) %>% 
summarise(mean_lifeExp=mean(lifeExp)) %>% 
  ggplot(aes(x=year,y=mean_lifeExp))+geom_point()
```

![](lab11_hw_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

**3. How do the distributions of life expectancy compare for the years 1952 and 2007?**

```r
gapminder %>% 
  filter(year==1952|year==2007) %>% 
  mutate(year=as.factor(year)) %>% 
  ggplot(aes(x=lifeExp,group=year,fill=year))+geom_boxplot()
```

![](lab11_hw_files/figure-html/unnamed-chunk-7-1.png)<!-- -->


**4. Your answer above doesn't tell the whole story since life expectancy varies by region. Make a summary that shows the min, mean, and max life expectancy by continent for all years represented in the data.**


```r
gapminder %>% 
  mutate(year=as.factor(year)) %>% 
  group_by(continent) %>% 
  summarise(min_LE=min(lifeExp),mean_LE=mean(lifeExp),max_LE=mean(lifeExp)) 
```

```
## # A tibble: 5 × 4
##   continent min_LE mean_LE max_LE
##   <fct>      <dbl>   <dbl>  <dbl>
## 1 Africa      23.6    48.9   48.9
## 2 Americas    37.6    64.7   64.7
## 3 Asia        28.8    60.1   60.1
## 4 Europe      43.6    71.9   71.9
## 5 Oceania     69.1    74.3   74.3
```
**5. How has life expectancy changed between 1952-2007 for each continent?**

```r
gapminder %>% 
  group_by(year,continent) %>% 
  summarise(mean=mean(lifeExp)) %>% 
  ggplot(aes(x=year,y=mean,group=continent,color=continent))+geom_line()
```

```
## `summarise()` has grouped output by 'year'. You can override using the
## `.groups` argument.
```

![](lab11_hw_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

**6. We are interested in the relationship between per capita GDP and life expectancy; i.e. does having more money help you live longer?**

```r
gapminder %>%
  ggplot(aes(x=lifeExp,y=gdpPercap))+geom_line()+scale_y_log10()+geom_smooth()
```

```
## `geom_smooth()` using method = 'gam' and formula = 'y ~ s(x, bs = "cs")'
```

![](lab11_hw_files/figure-html/unnamed-chunk-10-1.png)<!-- -->
**7. Which countries have had the largest population growth since 1952?**

```r
gapminder %>% 
  group_by(country) %>% 
  mutate("pop_growth"=max(gdpPercap)-min(gdpPercap)) %>% 
  arrange(desc(pop_growth)) %>% 
  select(country,pop_growth)
```

```
## # A tibble: 1,704 × 2
## # Groups:   country [142]
##    country pop_growth
##    <fct>        <dbl>
##  1 Kuwait      85405.
##  2 Kuwait      85405.
##  3 Kuwait      85405.
##  4 Kuwait      85405.
##  5 Kuwait      85405.
##  6 Kuwait      85405.
##  7 Kuwait      85405.
##  8 Kuwait      85405.
##  9 Kuwait      85405.
## 10 Kuwait      85405.
## # … with 1,694 more rows
```

```r
#Kuwait,Singapore,Norway,Hong Kong,Ireland
```

**8. Use your results from the question above to plot population growth for the top five countries since 1952.**

```r
#gapminder %>% 
#  filter(country=="Kuwait"|country=="Singapore"|country=="Norway"|country=="Hong Kong, China"|country=="Ireland") %>% 
#  group_by(year,gdpPercap) %>% 
#  summarise(n=n(), .groups='keep') %>% 
#  ggplot(aes(x=year, y=n, group=country, color=country))+
#  geom_line()+
#  geom_point(shape=2)+
#  theme(axis.text.x = element_text(angle = 60, hjust = 1))+
#  labs(title = "Number of samples for species DM & DS",
#       x = "Year",
#       fill = "n")
```

**9. How does per-capita GDP growth compare between these same five countries?**

```r
gapminder %>%  mutate("pop_growth"=max(gdpPercap)-min(gdpPercap)) %>% 
  group_by(country) %>% 
  mutate("pop_growth"=max(gdpPercap)-min(gdpPercap)) %>% 
  arrange(desc(pop_growth)) %>% 
 filter(country=="Kuwait"|country=="Singapore"|country=="Norway"|country=="Hong Kong, China"|country=="Ireland") %>% 
  ggplot(aes(x=country,y=pop_growth))+geom_col()
```

![](lab11_hw_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

**10. Make one plot of your choice that uses faceting!**



## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
