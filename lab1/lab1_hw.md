---
title: "Lab 1 Homework"
author: "David Galkowski"
date: "1-12-20"
output:
  html_document:
    keep_md: yes
    theme: spacelab
  pdf_document:
    toc: no
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run.  

1. Navigate to the R console and calculate the following expressions.  
  + 5 - 3 * 2    = -1
  + 8 / 2 ** 2   =  2

```r
5-3*2
```

```
## [1] -1
```


```r
8/2**2
```

```
## [1] 2
```
  
  
2. Did any of the results in #1 surprise you? Write two programs that calculate each expression such that the result for the first example is 4 and the second example is 16.  

```r
(5-3)*2
```

```
## [1] 4
```


```r
(8/2)**2
```

```
## [1] 16
```


The results of #1 make sense if you strictly follow math operations, but its confusing because my brain wants to do the math left to right.  

3. Make a new object `pi` as 3.14159265359.  


```r
pi <- 3.14159265359
```


4. Is `pi` an integer or numeric? Why? Show your code.  

'Pi' is numeric 

```r
is.numeric(pi)
```

```
## [1] TRUE
```


```r
is.integer(pi)
```

```
## [1] FALSE
```


```r
class(pi)
```

```
## [1] "numeric"
```


```r
my_missing <- NA
```


5. You have decided to use your new analytical powers in R to become a professional gambler. Here are your winnings and losses this week. Note that you don't gamble on the weekends!  

```r
blackjack <- c(140, -20, 70, -120, 240, NA, NA)
roulette <- c(60, 50, 120, -300, 10, NA, NA)
```

a. Build a new vector called `days` for the days of the week. 


```r
days <- c("monday", "tuesday", "wednesday", "thursday", "friday", "saturday", "sunday")
```


We will use `days` to name the elements in the poker and roulette vectors.

```r
names(blackjack) <- days
names(roulette) <- days
```

b. Calculate how much you won or lost in blackjack over the week.  


```r
sum(blackjack, na.rm = TRUE)
```

```
## [1] 310
```




c. What is your interpretation of this result? What do you need to do to address the problem? Recalculate how much you won or lost in blackjack over the week.  

The sum of the vector is "NA" because some of the vectors data is "NA", to adress the problem and calculate the sum of the blackjack vector, you need to adress missing data, and sum the vector withought its missing components.

d. Calculate how much you won or lost in roulette over the week.  

```r
sum(roulette, na.rm = TRUE)
```

```
## [1] -60
```


e. Build a `total_week` vector to show how much you lost or won on each day over the week. Which days seem lucky or unlucky for you?

```r
total_week <- c(blackjack+roulette)
```


```r
total_week[1]
```

```
## [1] 200
```

```r
total_week[2]
```

```
## [1] 30
```

```r
total_week[3]
```

```
## [1] 190
```

```r
total_week[4]
```

```
## [1] -420
```

```r
total_week[5]
```

```
## [1] 250
```

```r
total_week[6]
```

```
## [1] NA
```

```r
total_week[7]
```

```
## [1] NA
```
Thursday seems unlucky to me. 


f. Should you stick to blackjack or roulette? Write a program that verifies this below.  

```r
sum(blackjack, na.rm = TRUE)
```

```
## [1] 310
```

```r
sum(roulette, na.rm = TRUE)
```

```
## [1] -60
```


```r
blackjack>=roulette
```

```
## [1]  TRUE FALSE FALSE  TRUE  TRUE    NA    NA
```


```r
blackjack
```

```
## [1]  140  -20   70 -120  240   NA   NA
```

```r
roulette
```

```
## [1]   60   50  120 -300   10   NA   NA
```
three of five days, we made more money playing blackjack then roulette, and when we made more playing roulette, the difference between the outcomes was smaller. 


```r
mean(blackjack, na.rm = TRUE)
```

```
## [1] 62
```


```r
mean(roulette, na.rm = TRUE)
```

```
## [1] -12
```


```r
mean(blackjack, na.rm = TRUE) > mean(roulette, na.rm = TRUE)
```

```
## [1] TRUE
```

on average we made more playing blackjack. 

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  
