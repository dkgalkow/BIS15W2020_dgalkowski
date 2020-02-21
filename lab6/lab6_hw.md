---
title: "Lab 6 Homework"
author: "Please Add Your Name Here"
date: "Please Add the Date Here"
output:
  html_document: 
    keep_md: yes
    theme: spacelab
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run.  

## Libraries

```r
library(tidyverse)
```

## Resources
The idea for this assignment came from [Rebecca Barter's](http://www.rebeccabarter.com/blog/2017-11-17-ggplot2_tutorial/) ggplot tutorial so if you get stuck this is a good place to have a look.  

## Gapminder
For this assignment, we are going to use the dataset [gapminder](https://cran.r-project.org/web/packages/gapminder/index.html). Gapminder includes information about economics, population, and life expectancy from countries all over the world. You will need to install it before use. This is the same data that we used for the practice midterm. You may want to load that assignment for reference.  

```r
#install.packages("gapminder")
library("gapminder")
library("naniar")
```

## Questions
The questions below are open-ended and have many possible solutions. Your approach should, where appropriate, include numerical summaries and visuals. Be creative; assume you are building an analysis that you would ultimately present to an audience of stakeholders. Feel free to try out different `geoms` if they more clearly present your results.  

**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine how NAs are treated in the data.**  


```r
gapminder <- gapminder
```



```r
gapminder %>% 
  colnames() 
```

```
## [1] "country"   "continent" "year"      "lifeExp"   "pop"       "gdpPercap"
```

```r
gapminder
```

```
## # A tibble: 1,704 x 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Afghanistan Asia       1957    30.3  9240934      821.
##  3 Afghanistan Asia       1962    32.0 10267083      853.
##  4 Afghanistan Asia       1967    34.0 11537966      836.
##  5 Afghanistan Asia       1972    36.1 13079460      740.
##  6 Afghanistan Asia       1977    38.4 14880372      786.
##  7 Afghanistan Asia       1982    39.9 12881816      978.
##  8 Afghanistan Asia       1987    40.8 13867957      852.
##  9 Afghanistan Asia       1992    41.7 16317921      649.
## 10 Afghanistan Asia       1997    41.8 22227415      635.
## # … with 1,694 more rows
```


```r
gapminder %>% 
summarize(na_gapminder = sum(is.na(gapminder)))
```

```
## # A tibble: 1 x 1
##   na_gapminder
##          <int>
## 1            0
```



```r
gapminder %>% 
  naniar::miss_var_summary()
```

```
## # A tibble: 6 x 3
##   variable  n_miss pct_miss
##   <chr>      <int>    <dbl>
## 1 country        0        0
## 2 continent      0        0
## 3 year           0        0
## 4 lifeExp        0        0
## 5 pop            0        0
## 6 gdpPercap      0        0
```

```r
gapminder
```

```
## # A tibble: 1,704 x 6
##    country     continent  year lifeExp      pop gdpPercap
##    <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
##  1 Afghanistan Asia       1952    28.8  8425333      779.
##  2 Afghanistan Asia       1957    30.3  9240934      821.
##  3 Afghanistan Asia       1962    32.0 10267083      853.
##  4 Afghanistan Asia       1967    34.0 11537966      836.
##  5 Afghanistan Asia       1972    36.1 13079460      740.
##  6 Afghanistan Asia       1977    38.4 14880372      786.
##  7 Afghanistan Asia       1982    39.9 12881816      978.
##  8 Afghanistan Asia       1987    40.8 13867957      852.
##  9 Afghanistan Asia       1992    41.7 16317921      649.
## 10 Afghanistan Asia       1997    41.8 22227415      635.
## # … with 1,694 more rows
```


**2. Among the interesting variables in gapminder is life expectancy. How has global life expectancy changed between 1952 and 2007?**


```r
gapminder %>% 
  ggplot(aes(x=year, y=lifeExp))+
  geom_jitter()##for every country
```

![](lab6_hw_files/figure-html/unnamed-chunk-8-1.png)<!-- -->


```r
gapminder %>% 
  group_by(year) %>% 
  summarize(le_global= mean(lifeExp)) %>% 
  ggplot(aes(x=year, y=le_global))+
  geom_point()##as a mean of the countries' life expectancy.
```

![](lab6_hw_files/figure-html/unnamed-chunk-9-1.png)<!-- -->





**3. How do the distributions of life expectancy compare for the years 1952 and 2007? _Challenge: Can you put both distributions on a single plot?_**

```r
gapminder %>%
  filter(year== 1952 | year== 2007) %>% 
  ggplot(aes(x=country, y= lifeExp, fill= year))+
  geom_bar(stat= "identity")+
  coord_flip()
```

![](lab6_hw_files/figure-html/unnamed-chunk-10-1.png)<!-- -->


**4. Your answer above doesn't tell the whole story since life expectancy varies by region. Make a summary that shows the min, mean, and max life expectancy by continent for all years represented in the data.**


```r
gapminder %>% 
  ggplot(aes(x=continent, y=lifeExp, fill= year))+
  geom_boxplot()
```

![](lab6_hw_files/figure-html/unnamed-chunk-11-1.png)<!-- -->


```r
gapminder %>% 
  group_by(continent) %>% 
  summarise(min_le= min(lifeExp),
            mean_le= mean(lifeExp),
            max_le= max(lifeExp))
```

```
## # A tibble: 5 x 4
##   continent min_le mean_le max_le
##   <fct>      <dbl>   <dbl>  <dbl>
## 1 Africa      23.6    48.9   76.4
## 2 Americas    37.6    64.7   80.7
## 3 Asia        28.8    60.1   82.6
## 4 Europe      43.6    71.9   81.8
## 5 Oceania     69.1    74.3   81.2
```



**5. How has life expectancy changed between 1952-2007 for each continent? Try using `geom_line()` for this, including all continents on the same  plot.**

```r
gapminder %>% 
  select(continent, lifeExp, year) %>% 
  group_by(continent,year) %>% 
  summarise(avg_le= mean(lifeExp)) %>% 
  ggplot(aes(x=year, y=avg_le, color= continent))+
  geom_line()
```

![](lab6_hw_files/figure-html/unnamed-chunk-13-1.png)<!-- -->


**6. We are interested in the relationship between per capita GDP and life expectancy; i.e. does having more money help you live longer?**


```r
gapminder %>% 
  group_by(year) %>%
  summarise(gdp_av= mean(gdpPercap), Le_av= mean(lifeExp)) %>% 
  ggplot(aes(x= gdp_av, y= Le_av, color= year))+
  geom_line()
```

![](lab6_hw_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

**7. There is extreme disparity in per capita GDP. Rescale the x axis to make this easier to interpret. How would you characterize the relationship?**


```r
gapminder %>% 
  group_by(year) %>%
  summarise(gdp_av= mean(gdpPercap), av_le= mean(lifeExp)) %>% 
  ggplot(aes(x= gdp_av, y= av_le, color= year))+
  geom_line()+
  scale_x_log10()
```

![](lab6_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->


**8. Which countries have had the largest population growth since 1952?**

```r
gapminder %>% 
  group_by(country) %>% 
  summarise(popchng = max(pop)-min(pop)) %>% 
  arrange(desc(popchng)) %>%
  filter(popchng>= 133408087)
```

```
## # A tibble: 5 x 2
##   country         popchng
##   <fct>             <int>
## 1 China         762419569
## 2 India         738396331
## 3 United States 143586947
## 4 Indonesia     141495000
## 5 Brazil        133408087
```

```r
gapminder %>% 
  group_by(country) %>% 
  summarise(popchng = max(pop)-min(pop)) %>% 
  arrange(desc(popchng)) %>%
  filter(popchng>= 133408087) %>% 
  ggplot(aes(x=country, y=popchng, fill= country))+
  geom_bar(stat = "identity")+
  coord_flip()+
  theme(axis.text.x = element_text(angle = 60, hjust = 1))
```

![](lab6_hw_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

```r
  ##china,india,US, and Indonesia have grown the most. 
```


**9. Use your results from the question above to plot population growth for the top five countries since 1952.**

```r
gapminder %>% 
  group_by(country) %>% 
  summarise(popchng = max(pop)-min(pop)) %>% 
  arrange(desc(popchng)) %>%
  filter(popchng>= 133408087) %>% 
  ggplot(aes(x=country, y=popchng, fill= country))+
  geom_bar(stat = "identity")+
  coord_flip()+
  theme(axis.text.x = element_text(angle = 60, hjust = 1))
```

![](lab6_hw_files/figure-html/unnamed-chunk-17-1.png)<!-- -->


**10. How does per capita GDP growth compare between these same five countries?**

```r
gapminder %>% 
  filter(country == "India" | country == "China" | country == "United States" | country == "Indonesia") %>% 
  group_by(country) %>% 
  summarise(gdpchng= last(gdpPercap)- first(gdpPercap)) 
```

```
## # A tibble: 4 x 2
##   country       gdpchng
##   <fct>           <dbl>
## 1 China           4559.
## 2 India           1906.
## 3 Indonesia       2791.
## 4 United States  28961.
```

```r
gapminder %>% 
  filter(country == "India" | country == "China" | country == "United States" | country == "Indonesia") %>% 
  group_by(country) %>% 
  summarise(gdpchng= last(gdpPercap)- first(gdpPercap)) %>% 
  ggplot(aes(x=country, y= gdpchng, fill= country))+
  geom_bar(stat= "identity")+
  coord_flip()+
  theme(axis.text.x = element_text(angle=60, hjust= 1))
```

![](lab6_hw_files/figure-html/unnamed-chunk-18-1.png)<!-- -->



## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
