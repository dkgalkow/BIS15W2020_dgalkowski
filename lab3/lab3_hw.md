---
title: "Lab 3 Homework"
author: "Please Add Your Name Here"
date: "Winter 2020"
output:
  html_document:
    keep_md: yes
    theme: spacelab
---

```r
getwd()
```

```
## [1] "/Users/davidgalkowski/Downloads/BIS15W2020_dgalkowski-master/lab3"
```



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run.  

## Load the tidyverse

```r
library(tidyverse)
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

1. Load the data into a new object called `homerange`.  

```r
homerange <- readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   mean.mass.g = col_double(),
##   log10.mass = col_double(),
##   mean.hra.m2 = col_double(),
##   log10.hra = col_double(),
##   preymass = col_double(),
##   log10.preymass = col_double(),
##   PPMR = col_double()
## )
```

```
## See spec(...) for full column specifications.
```

2. Use `spec()` to see the full details of the columns.  

```r
spec(homerange)
```

```
## cols(
##   taxon = col_character(),
##   common.name = col_character(),
##   class = col_character(),
##   order = col_character(),
##   family = col_character(),
##   genus = col_character(),
##   species = col_character(),
##   primarymethod = col_character(),
##   N = col_character(),
##   mean.mass.g = col_double(),
##   log10.mass = col_double(),
##   alternative.mass.reference = col_character(),
##   mean.hra.m2 = col_double(),
##   log10.hra = col_double(),
##   hra.reference = col_character(),
##   realm = col_character(),
##   thermoregulation = col_character(),
##   locomotion = col_character(),
##   trophic.guild = col_character(),
##   dimension = col_character(),
##   preymass = col_double(),
##   log10.preymass = col_double(),
##   PPMR = col_double(),
##   prey.size.reference = col_character()
## )
```

3. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.  

```r
dim(homerange)
```

```
## [1] 569  24
```


```r
colnames(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```


```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild       dimension            preymass         log10.preymass   
##  Length:569         Length:569         Min.   :     0.67   Min.   :-0.1739  
##  Class :character   Class :character   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Mode  :character   Median :    53.75   Median : 1.7304  
##                                        Mean   :  3989.88   Mean   : 2.0188  
##                                        3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                                        Max.   :130233.20   Max.   : 5.1147  
##                                        NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```


4. Are there NA's in your data? Show the code that you would use to verify this, please.  

```r
anyNA(homerange)
```

```
## [1] TRUE
```

5. Change the class of the variables `taxon` and `order` to factors and display their levels.  


```r
class(homerange$taxon)
```

```
## [1] "character"
```

```r
class(homerange$order)
```

```
## [1] "character"
```


```r
homerange$taxon <- as.factor(homerange$taxon)
class(homerange$taxon)
```

```
## [1] "factor"
```

```r
homerange$order <- as.factor(homerange$order)
class(homerange$order)
```

```
## [1] "factor"
```


```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"    "afrosoricida"       "anguilliformes"    
##  [4] "anseriformes"       "apterygiformes"     "artiodactyla"      
##  [7] "caprimulgiformes"   "carnivora"          "charadriiformes"   
## [10] "columbidormes"      "columbiformes"      "coraciiformes"     
## [13] "cuculiformes"       "cypriniformes"      "dasyuromorpha"     
## [16] "dasyuromorpia"      "didelphimorphia"    "diprodontia"       
## [19] "diprotodontia"      "erinaceomorpha"     "esociformes"       
## [22] "falconiformes"      "gadiformes"         "galliformes"       
## [25] "gruiformes"         "lagomorpha"         "macroscelidea"     
## [28] "monotrematae"       "passeriformes"      "pelecaniformes"    
## [31] "peramelemorphia"    "perciformes"        "perissodactyla"    
## [34] "piciformes"         "pilosa"             "proboscidea"       
## [37] "psittaciformes"     "rheiformes"         "roden"             
## [40] "rodentia"           "salmoniformes"      "scorpaeniformes"   
## [43] "siluriformes"       "soricomorpha"       "squamata"          
## [46] "strigiformes"       "struthioniformes"   "syngnathiformes"   
## [49] "testudines"         "tetraodontiformes\xa0" "tinamiformes"
```


6. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer?  

```r
colnames(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```


```r
deer<- homerange %>% 
  select(mean.mass.g, log10.mass, family, genus, species) %>% 
  filter(family == "cervidae") %>% 
  arrange(desc(log10.mass))

deer
```

```
## # A tibble: 12 x 5
##    mean.mass.g log10.mass family   genus      species    
##          <dbl>      <dbl> <chr>    <chr>      <chr>      
##  1     307227.       5.49 cervidae alces      alces      
##  2     234758.       5.37 cervidae cervus     elaphus    
##  3     102059.       5.01 cervidae rangifer   tarandus   
##  4      87884.       4.94 cervidae odocoileus virginianus
##  5      71450.       4.85 cervidae dama       dama       
##  6      62823.       4.80 cervidae axis       axis       
##  7      53864.       4.73 cervidae odocoileus hemionus   
##  8      35000.       4.54 cervidae ozotoceros bezoarticus
##  9      29450.       4.47 cervidae cervus     nippon     
## 10      24050.       4.38 cervidae capreolus  capreolus  
## 11      13500.       4.13 cervidae muntiacus  reevesi    
## 12       7500.       3.88 cervidae pudu       puda
```


##The largest deer is "alces alces""

7. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!  


```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```


```r
funtubes <-
homerange %>% 
  filter(taxon == "snakes") %>% 
  select(mean.hra.m2, family, genus, species) %>% 
  arrange(mean.hra.m2)

funtubes
```

```
## # A tibble: 41 x 4
##    mean.hra.m2 family     genus       species     
##          <dbl> <chr>      <chr>       <chr>       
##  1        200  viperidae  bitis       schneideri  
##  2        253  colubridae carphopis   viridis     
##  3        600  colubridae thamnophis  butleri     
##  4        700  colubridae carphopis   vermis      
##  5       2400  viperidae  vipera      latastei    
##  6       2614. viperidae  gloydius    shedaoensis 
##  7       6476  colubridae diadophis   punctatus   
##  8      10655  viperidae  agkistrodon piscivorous 
##  9      15400  colubridae oocatochus  rufodorsatus
## 10      17400  colubridae pituophis   catenifer   
## # … with 31 more rows
```

##Bitis schneideri is a venomous viper species found in a small coastal region that straddles the border between Namibia and South Africa. This is the smallest species in the genus Bitis and possibly the world's smallest viper.

8. You suspect that homerange and mass are correlated in birds. We need a ratio that facilitates exploration of this prediction. First, build a new dataframe called `hra_ratio` that is limited to genus, species, mean.mass.g, log10.mass, log10.hra. Arrange it in ascending order by mean mass in grams.  


```r
hra_ratio <-
  homerange %>% 
  select(genus, species, mean.mass.g, log10.mass, log10.hra) %>% 
  arrange(mean.mass.g)
  
hra_ratio
```

```
## # A tibble: 569 x 5
##    genus          species        mean.mass.g log10.mass log10.hra
##    <chr>          <chr>                <dbl>      <dbl>     <dbl>
##  1 priolepis      hipoliti              0.22    -0.658    -1.52  
##  2 lythrypnus     dalli                 0.31    -0.509    -0.301 
##  3 amblycirrhitus pinos                 0.45    -0.347     0.405 
##  4 nerophis       lumbriciformis        1.22     0.0864    1.10  
##  5 salmo          salar                 2        0.301     1.65  
##  6 centropyge     argi                  2.5      0.398     0.0531
##  7 amblyeleotris  japonica              2.7      0.431     1.45  
##  8 cottus         carolinae             3        0.477     1.67  
##  9 thalassoma     bifasciatum           3.12     0.494     2.01  
## 10 carphopis      vermis                3.46     0.539     2.85  
## # … with 559 more rows
```

9. Replace the existing `hra_ratio` dataframe with a new dataframe that adds a column calculating the ratio of log 10 hra to log 10 mass. Call it `hra.mass.ratio`. Arrange it in descending order by mean mass in grams.  


```r
hra_ratio <-
  hra_ratio %>% 
  mutate(hra.mass.ratio = log10.hra/log10.mass) %>% 
  arrange(desc(mean.mass.g))

hra_ratio
```

```
## # A tibble: 569 x 6
##    genus         species        mean.mass.g log10.mass log10.hra hra.mass.ratio
##    <chr>         <chr>                <dbl>      <dbl>     <dbl>          <dbl>
##  1 elephas       maximus           4000000.       6.60      8.04           1.22
##  2 loxodonta     africana          4000000.       6.60      9.24           1.40
##  3 ceratotherium simum             2249987.       6.35      7.20           1.13
##  4 giraffa       camelopardalis    1339985.       6.13      8.14           1.33
##  5 diceros       bicornis          1050002.       6.02      7.62           1.27
##  6 taurotragus   oryx               635038.       5.80      7.72           1.33
##  7 bison         bison              629999.       5.80      8.42           1.45
##  8 oreamnos      americanus         629999.       5.80      7.37           1.27
##  9 bison         bonasus            628001.       5.80      7.01           1.21
## 10 equus         caballus           427996.       5.63      7.35           1.30
## # … with 559 more rows
```

10. What is the lowest mass for birds with a `hra.mass.ratio` greater than or equal to 4.0?


```r
homerange %>%
  mutate(hra.mass.ratio = log10.hra/log10.mass) %>% 
  filter(taxon == "birds" & hra.mass.ratio >= 4.0) %>% 
  arrange(mean.mass.g) %>% 
  select(taxon, genus, species, hra.mass.ratio, mean.mass.g)
```

```
## # A tibble: 17 x 5
##    taxon genus        species      hra.mass.ratio mean.mass.g
##    <fct> <chr>        <chr>                 <dbl>       <dbl>
##  1 birds regulus      regulus                6.04        5.15
##  2 birds regulus      ignicapillus           5.82        5.3 
##  3 birds phylloscopus bonelli                5.19        7.5 
##  4 birds aegithalos   caudatus               5.12        8   
##  5 birds vireo        atricapillus           4.49        8.5 
##  6 birds setophaga    magnolia               4.13        8.6 
##  7 birds certhia      familiaris             4.95        8.77
##  8 birds wilsonia     canadensis             4.14        9.3 
##  9 birds troglodytes  troglodytes            4.10        9.5 
## 10 birds cisticola    juncidis               4.20        9.8 
## 11 birds vireo        belli                  4.07       10   
## 12 birds parus        carolinensis           4.16       10.1 
## 13 birds hippolais    polyglotta             4.30       11   
## 14 birds parus        palustris              4.18       11   
## 15 birds spizella     passerina              4.13       12.2 
## 16 birds contopus     virens                 4.07       13.8 
## 17 birds motacilla    alba                   4.44       21.2
```
##lowest mean mass(g) = 5.15g

11. Do a search online; what is the common name of the bird from #8 above? Place a link in your markdown file that takes us to a webpage with information on its biology. 

##regulus regulus: goldcrest

12. What is the `hra.mass.ratio` for an ostrich? Show your work, please. 


```r
homerange %>% 
  mutate(hra.mass.ratio = log10.hra/log10.mass) %>% 
  select(hra.mass.ratio, common.name) %>% 
  filter(common.name == "ostrich")
```

```
## # A tibble: 1 x 2
##   hra.mass.ratio common.name
##            <dbl> <chr>      
## 1           1.60 ostrich
```
##hra mass ratio is 1.602565 for an ostrich. 

## Push your final code to GitHub!
Please be sure that you have check the `keep md` file in the knit preferences.  
