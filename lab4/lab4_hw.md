---
title: "Lab 4 Homework"
author: "David Galkowski"
date: "2/7/20"
output:
  html_document: 
    keep_md: yes
    theme: spacelab
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove any `#` for included code chunks to run.  

## Load the tidyverse

```r
library(tidyverse)
```

For this assignment we are going to work with a large dataset from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. First, load the data.  

1. Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries<- readr::read_csv("data/FAO_1950to2012_111914.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   `ISSCAAP group#` = col_double(),
##   `FAO major fishing area` = col_double()
## )
```

```
## See spec(...) for full column specifications.
```


2. What are the names of the columns? Do you see any potential problems with the column names?

```r
colnames(fisheries)
```

```
##  [1] "Country"                 "Common name"            
##  [3] "ISSCAAP group#"          "ISSCAAP taxonomic group"
##  [5] "ASFIS species#"          "ASFIS species name"     
##  [7] "FAO major fishing area"  "Measure"                
##  [9] "1950"                    "1951"                   
## [11] "1952"                    "1953"                   
## [13] "1954"                    "1955"                   
## [15] "1956"                    "1957"                   
## [17] "1958"                    "1959"                   
## [19] "1960"                    "1961"                   
## [21] "1962"                    "1963"                   
## [23] "1964"                    "1965"                   
## [25] "1966"                    "1967"                   
## [27] "1968"                    "1969"                   
## [29] "1970"                    "1971"                   
## [31] "1972"                    "1973"                   
## [33] "1974"                    "1975"                   
## [35] "1976"                    "1977"                   
## [37] "1978"                    "1979"                   
## [39] "1980"                    "1981"                   
## [41] "1982"                    "1983"                   
## [43] "1984"                    "1985"                   
## [45] "1986"                    "1987"                   
## [47] "1988"                    "1989"                   
## [49] "1990"                    "1991"                   
## [51] "1992"                    "1993"                   
## [53] "1994"                    "1995"                   
## [55] "1996"                    "1997"                   
## [57] "1998"                    "1999"                   
## [59] "2000"                    "2001"                   
## [61] "2002"                    "2003"                   
## [63] "2004"                    "2005"                   
## [65] "2006"                    "2007"                   
## [67] "2008"                    "2009"                   
## [69] "2010"                    "2011"                   
## [71] "2012"
```
##there are alot of 'year' column names and this could be a problem because R likes data to be in the format where there is one column for year and then all the observations are in rows. 

3. What is the structure of the data? Show the classes of each variable.

```r
summary(fisheries)
```

```
##    Country          Common name        ISSCAAP group#  ISSCAAP taxonomic group
##  Length:17692       Length:17692       Min.   :11.00   Length:17692           
##  Class :character   Class :character   1st Qu.:33.00   Class :character       
##  Mode  :character   Mode  :character   Median :36.00   Mode  :character       
##                                        Mean   :37.38                          
##                                        3rd Qu.:38.00                          
##                                        Max.   :77.00                          
##  ASFIS species#     ASFIS species name FAO major fishing area
##  Length:17692       Length:17692       Min.   :18.00         
##  Class :character   Class :character   1st Qu.:31.00         
##  Mode  :character   Mode  :character   Median :37.00         
##                                        Mean   :45.34         
##                                        3rd Qu.:57.00         
##                                        Max.   :88.00         
##    Measure              1950               1951               1952          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1953               1954               1955               1956          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1957               1958               1959               1960          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1961               1962               1963               1964          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1965               1966               1967               1968          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1969               1970               1971               1972          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1973               1974               1975               1976          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1977               1978               1979               1980          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1981               1982               1983               1984          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1985               1986               1987               1988          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1989               1990               1991               1992          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1993               1994               1995               1996          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      1997               1998               1999               2000          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2001               2002               2003               2004          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2005               2006               2007               2008          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##      2009               2010               2011               2012          
##  Length:17692       Length:17692       Length:17692       Length:17692      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
## 
```
##every column class is a character. 

4. Think about the classes. Will any present problems? Make any changes you think are necessary below.
##everything needs to be a factor for some reason


```r
fisheries$Country<- as.factor(fisheries$Country)
fisheries$`Common name`<-as.factor(fisheries$`Common name`)
```


5. How many countries are represented in the data? Provide a count.

```r
levels(fisheries$Country)
```

```
##   [1] "Albania"                   "Algeria"                  
##   [3] "American Samoa"            "Angola"                   
##   [5] "Anguilla"                  "Antigua and Barbuda"      
##   [7] "Argentina"                 "Aruba"                    
##   [9] "Australia"                 "Bahamas"                  
##  [11] "Bahrain"                   "Bangladesh"               
##  [13] "Barbados"                  "Belgium"                  
##  [15] "Belize"                    "Benin"                    
##  [17] "Bermuda"                   "Bonaire/S.Eustatius/Saba" 
##  [19] "Bosnia and Herzegovina"    "Brazil"                   
##  [21] "British Indian Ocean Ter"  "British Virgin Islands"   
##  [23] "Brunei Darussalam"         "Bulgaria"                 
##  [25] "Cabo Verde"                "Cambodia"                 
##  [27] "Cameroon"                  "Canada"                   
##  [29] "Cayman Islands"            "Channel Islands"          
##  [31] "Chile"                     "China"                    
##  [33] "China, Hong Kong SAR"      "China, Macao SAR"         
##  [35] "Colombia"                  "Comoros"                  
##  [37] "Congo, Dem. Rep. of the"   "Congo, Republic of"       
##  [39] "Cook Islands"              "Costa Rica"               
##  [41] "Croatia"                   "Cuba"                     
##  [43] "Cura\xe7ao"                "Cyprus"                   
##  [45] "C\xf4te d'Ivoire"          "Denmark"                  
##  [47] "Djibouti"                  "Dominica"                 
##  [49] "Dominican Republic"        "Ecuador"                  
##  [51] "Egypt"                     "El Salvador"              
##  [53] "Equatorial Guinea"         "Eritrea"                  
##  [55] "Estonia"                   "Ethiopia"                 
##  [57] "Falkland Is.(Malvinas)"    "Faroe Islands"            
##  [59] "Fiji, Republic of"         "Finland"                  
##  [61] "France"                    "French Guiana"            
##  [63] "French Polynesia"          "French Southern Terr"     
##  [65] "Gabon"                     "Gambia"                   
##  [67] "Georgia"                   "Germany"                  
##  [69] "Ghana"                     "Gibraltar"                
##  [71] "Greece"                    "Greenland"                
##  [73] "Grenada"                   "Guadeloupe"               
##  [75] "Guam"                      "Guatemala"                
##  [77] "Guinea"                    "GuineaBissau"             
##  [79] "Guyana"                    "Haiti"                    
##  [81] "Honduras"                  "Iceland"                  
##  [83] "India"                     "Indonesia"                
##  [85] "Iran (Islamic Rep. of)"    "Iraq"                     
##  [87] "Ireland"                   "Isle of Man"              
##  [89] "Israel"                    "Italy"                    
##  [91] "Jamaica"                   "Japan"                    
##  [93] "Jordan"                    "Kenya"                    
##  [95] "Kiribati"                  "Korea, Dem. People's Rep" 
##  [97] "Korea, Republic of"        "Kuwait"                   
##  [99] "Latvia"                    "Lebanon"                  
## [101] "Liberia"                   "Libya"                    
## [103] "Lithuania"                 "Madagascar"               
## [105] "Malaysia"                  "Maldives"                 
## [107] "Malta"                     "Marshall Islands"         
## [109] "Martinique"                "Mauritania"               
## [111] "Mauritius"                 "Mayotte"                  
## [113] "Mexico"                    "Micronesia, Fed.States of"
## [115] "Monaco"                    "Montenegro"               
## [117] "Montserrat"                "Morocco"                  
## [119] "Mozambique"                "Myanmar"                  
## [121] "Namibia"                   "Nauru"                    
## [123] "Netherlands"               "Netherlands Antilles"     
## [125] "New Caledonia"             "New Zealand"              
## [127] "Nicaragua"                 "Nigeria"                  
## [129] "Niue"                      "Norfolk Island"           
## [131] "Northern Mariana Is."      "Norway"                   
## [133] "Oman"                      "Other nei"                
## [135] "Pakistan"                  "Palau"                    
## [137] "Palestine, Occupied Tr."   "Panama"                   
## [139] "Papua New Guinea"          "Peru"                     
## [141] "Philippines"               "Pitcairn Islands"         
## [143] "Poland"                    "Portugal"                 
## [145] "Puerto Rico"               "Qatar"                    
## [147] "Romania"                   "Russian Federation"       
## [149] "R\xe9union"                "Saint Barth\xe9lemy"      
## [151] "Saint Helena"              "Saint Kitts and Nevis"    
## [153] "Saint Lucia"               "Saint Vincent/Grenadines" 
## [155] "SaintMartin"               "Samoa"                    
## [157] "Sao Tome and Principe"     "Saudi Arabia"             
## [159] "Senegal"                   "Serbia and Montenegro"    
## [161] "Seychelles"                "Sierra Leone"             
## [163] "Singapore"                 "Sint Maarten"             
## [165] "Slovenia"                  "Solomon Islands"          
## [167] "Somalia"                   "South Africa"             
## [169] "Spain"                     "Sri Lanka"                
## [171] "St. Pierre and Miquelon"   "Sudan"                    
## [173] "Sudan (former)"            "Suriname"                 
## [175] "Svalbard and Jan Mayen"    "Sweden"                   
## [177] "Syrian Arab Republic"      "Taiwan Province of China" 
## [179] "Tanzania, United Rep. of"  "Thailand"                 
## [181] "TimorLeste"                "Togo"                     
## [183] "Tokelau"                   "Tonga"                    
## [185] "Trinidad and Tobago"       "Tunisia"                  
## [187] "Turkey"                    "Turks and Caicos Is."     
## [189] "Tuvalu"                    "Ukraine"                  
## [191] "Un. Sov. Soc. Rep."        "United Arab Emirates"     
## [193] "United Kingdom"            "United States of America" 
## [195] "Uruguay"                   "US Virgin Islands"        
## [197] "Vanuatu"                   "Venezuela, Boliv Rep of"  
## [199] "Viet Nam"                  "Wallis and Futuna Is."    
## [201] "Western Sahara"            "Yemen"                    
## [203] "Yugoslavia SFR"            "Zanzibar"
```
##there are 204 countries

6. What are the names of the countries?


```r
levels(fisheries$Country)
```

```
##   [1] "Albania"                   "Algeria"                  
##   [3] "American Samoa"            "Angola"                   
##   [5] "Anguilla"                  "Antigua and Barbuda"      
##   [7] "Argentina"                 "Aruba"                    
##   [9] "Australia"                 "Bahamas"                  
##  [11] "Bahrain"                   "Bangladesh"               
##  [13] "Barbados"                  "Belgium"                  
##  [15] "Belize"                    "Benin"                    
##  [17] "Bermuda"                   "Bonaire/S.Eustatius/Saba" 
##  [19] "Bosnia and Herzegovina"    "Brazil"                   
##  [21] "British Indian Ocean Ter"  "British Virgin Islands"   
##  [23] "Brunei Darussalam"         "Bulgaria"                 
##  [25] "Cabo Verde"                "Cambodia"                 
##  [27] "Cameroon"                  "Canada"                   
##  [29] "Cayman Islands"            "Channel Islands"          
##  [31] "Chile"                     "China"                    
##  [33] "China, Hong Kong SAR"      "China, Macao SAR"         
##  [35] "Colombia"                  "Comoros"                  
##  [37] "Congo, Dem. Rep. of the"   "Congo, Republic of"       
##  [39] "Cook Islands"              "Costa Rica"               
##  [41] "Croatia"                   "Cuba"                     
##  [43] "Cura\xe7ao"                "Cyprus"                   
##  [45] "C\xf4te d'Ivoire"          "Denmark"                  
##  [47] "Djibouti"                  "Dominica"                 
##  [49] "Dominican Republic"        "Ecuador"                  
##  [51] "Egypt"                     "El Salvador"              
##  [53] "Equatorial Guinea"         "Eritrea"                  
##  [55] "Estonia"                   "Ethiopia"                 
##  [57] "Falkland Is.(Malvinas)"    "Faroe Islands"            
##  [59] "Fiji, Republic of"         "Finland"                  
##  [61] "France"                    "French Guiana"            
##  [63] "French Polynesia"          "French Southern Terr"     
##  [65] "Gabon"                     "Gambia"                   
##  [67] "Georgia"                   "Germany"                  
##  [69] "Ghana"                     "Gibraltar"                
##  [71] "Greece"                    "Greenland"                
##  [73] "Grenada"                   "Guadeloupe"               
##  [75] "Guam"                      "Guatemala"                
##  [77] "Guinea"                    "GuineaBissau"             
##  [79] "Guyana"                    "Haiti"                    
##  [81] "Honduras"                  "Iceland"                  
##  [83] "India"                     "Indonesia"                
##  [85] "Iran (Islamic Rep. of)"    "Iraq"                     
##  [87] "Ireland"                   "Isle of Man"              
##  [89] "Israel"                    "Italy"                    
##  [91] "Jamaica"                   "Japan"                    
##  [93] "Jordan"                    "Kenya"                    
##  [95] "Kiribati"                  "Korea, Dem. People's Rep" 
##  [97] "Korea, Republic of"        "Kuwait"                   
##  [99] "Latvia"                    "Lebanon"                  
## [101] "Liberia"                   "Libya"                    
## [103] "Lithuania"                 "Madagascar"               
## [105] "Malaysia"                  "Maldives"                 
## [107] "Malta"                     "Marshall Islands"         
## [109] "Martinique"                "Mauritania"               
## [111] "Mauritius"                 "Mayotte"                  
## [113] "Mexico"                    "Micronesia, Fed.States of"
## [115] "Monaco"                    "Montenegro"               
## [117] "Montserrat"                "Morocco"                  
## [119] "Mozambique"                "Myanmar"                  
## [121] "Namibia"                   "Nauru"                    
## [123] "Netherlands"               "Netherlands Antilles"     
## [125] "New Caledonia"             "New Zealand"              
## [127] "Nicaragua"                 "Nigeria"                  
## [129] "Niue"                      "Norfolk Island"           
## [131] "Northern Mariana Is."      "Norway"                   
## [133] "Oman"                      "Other nei"                
## [135] "Pakistan"                  "Palau"                    
## [137] "Palestine, Occupied Tr."   "Panama"                   
## [139] "Papua New Guinea"          "Peru"                     
## [141] "Philippines"               "Pitcairn Islands"         
## [143] "Poland"                    "Portugal"                 
## [145] "Puerto Rico"               "Qatar"                    
## [147] "Romania"                   "Russian Federation"       
## [149] "R\xe9union"                "Saint Barth\xe9lemy"      
## [151] "Saint Helena"              "Saint Kitts and Nevis"    
## [153] "Saint Lucia"               "Saint Vincent/Grenadines" 
## [155] "SaintMartin"               "Samoa"                    
## [157] "Sao Tome and Principe"     "Saudi Arabia"             
## [159] "Senegal"                   "Serbia and Montenegro"    
## [161] "Seychelles"                "Sierra Leone"             
## [163] "Singapore"                 "Sint Maarten"             
## [165] "Slovenia"                  "Solomon Islands"          
## [167] "Somalia"                   "South Africa"             
## [169] "Spain"                     "Sri Lanka"                
## [171] "St. Pierre and Miquelon"   "Sudan"                    
## [173] "Sudan (former)"            "Suriname"                 
## [175] "Svalbard and Jan Mayen"    "Sweden"                   
## [177] "Syrian Arab Republic"      "Taiwan Province of China" 
## [179] "Tanzania, United Rep. of"  "Thailand"                 
## [181] "TimorLeste"                "Togo"                     
## [183] "Tokelau"                   "Tonga"                    
## [185] "Trinidad and Tobago"       "Tunisia"                  
## [187] "Turkey"                    "Turks and Caicos Is."     
## [189] "Tuvalu"                    "Ukraine"                  
## [191] "Un. Sov. Soc. Rep."        "United Arab Emirates"     
## [193] "United Kingdom"            "United States of America" 
## [195] "Uruguay"                   "US Virgin Islands"        
## [197] "Vanuatu"                   "Venezuela, Boliv Rep of"  
## [199] "Viet Nam"                  "Wallis and Futuna Is."    
## [201] "Western Sahara"            "Yemen"                    
## [203] "Yugoslavia SFR"            "Zanzibar"
```


7. Use `rename()` to rename the columns and make them easier to use. The new column names should be:  
+ country
+ commname
+ ASFIS_sciname
+ ASFIS_spcode
+ ISSCAAP_spgroup
+ ISSCAAP_spgroupname
+ FAO_area
+ unit

```r
colnames(fisheries)
```

```
##  [1] "Country"                 "Common name"            
##  [3] "ISSCAAP group#"          "ISSCAAP taxonomic group"
##  [5] "ASFIS species#"          "ASFIS species name"     
##  [7] "FAO major fishing area"  "Measure"                
##  [9] "1950"                    "1951"                   
## [11] "1952"                    "1953"                   
## [13] "1954"                    "1955"                   
## [15] "1956"                    "1957"                   
## [17] "1958"                    "1959"                   
## [19] "1960"                    "1961"                   
## [21] "1962"                    "1963"                   
## [23] "1964"                    "1965"                   
## [25] "1966"                    "1967"                   
## [27] "1968"                    "1969"                   
## [29] "1970"                    "1971"                   
## [31] "1972"                    "1973"                   
## [33] "1974"                    "1975"                   
## [35] "1976"                    "1977"                   
## [37] "1978"                    "1979"                   
## [39] "1980"                    "1981"                   
## [41] "1982"                    "1983"                   
## [43] "1984"                    "1985"                   
## [45] "1986"                    "1987"                   
## [47] "1988"                    "1989"                   
## [49] "1990"                    "1991"                   
## [51] "1992"                    "1993"                   
## [53] "1994"                    "1995"                   
## [55] "1996"                    "1997"                   
## [57] "1998"                    "1999"                   
## [59] "2000"                    "2001"                   
## [61] "2002"                    "2003"                   
## [63] "2004"                    "2005"                   
## [65] "2006"                    "2007"                   
## [67] "2008"                    "2009"                   
## [69] "2010"                    "2011"                   
## [71] "2012"
```


```r
fisheries2<- 
fisheries %>%
  rename(
    "country"=Country,
    "commname"=`Common name`,
    "ASFIS_sciname"=`ASFIS species name`,
    "ASFIS_spcode"=`ASFIS species#`,
    "ISSCAAP_spgroup"=`ISSCAAP group#`,
    "ISSCAAP_spgroupname"=`ISSCAAP taxonomic group`,
    "FAO_area"=`FAO major fishing area`,
    "unit"=Measure)
fisheries2
```

```
## # A tibble: 17,692 x 71
##    country commname ISSCAAP_spgroup ISSCAAP_spgroup… ASFIS_spcode ASFIS_sciname
##    <fct>   <fct>              <dbl> <chr>            <chr>        <chr>        
##  1 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  2 Albania Atlanti…              36 Tunas, bonitos,… 1750100101   Sarda sarda  
##  3 Albania Barracu…              37 Miscellaneous p… 17710001XX   Sphyraena spp
##  4 Albania Blue an…              45 Shrimps, prawns  2280203101   Aristeus ant…
##  5 Albania Blue wh…              32 Cods, hakes, ha… 1480403301   Micromesisti…
##  6 Albania Bluefish              37 Miscellaneous p… 1702021301   Pomatomus sa…
##  7 Albania Bogue                 33 Miscellaneous c… 1703926101   Boops boops  
##  8 Albania Caramot…              45 Shrimps, prawns  2280100117   Penaeus kera…
##  9 Albania Catshar…              38 Sharks, rays, c… 10801003XX   Scyliorhinus…
## 10 Albania Common …              57 Squids, cuttlef… 3210200202   Sepia offici…
## # … with 17,682 more rows, and 65 more variables: FAO_area <dbl>, unit <chr>,
## #   `1950` <chr>, `1951` <chr>, `1952` <chr>, `1953` <chr>, `1954` <chr>,
## #   `1955` <chr>, `1956` <chr>, `1957` <chr>, `1958` <chr>, `1959` <chr>,
## #   `1960` <chr>, `1961` <chr>, `1962` <chr>, `1963` <chr>, `1964` <chr>,
## #   `1965` <chr>, `1966` <chr>, `1967` <chr>, `1968` <chr>, `1969` <chr>,
## #   `1970` <chr>, `1971` <chr>, `1972` <chr>, `1973` <chr>, `1974` <chr>,
## #   `1975` <chr>, `1976` <chr>, `1977` <chr>, `1978` <chr>, `1979` <chr>,
## #   `1980` <chr>, `1981` <chr>, `1982` <chr>, `1983` <chr>, `1984` <chr>,
## #   `1985` <chr>, `1986` <chr>, `1987` <chr>, `1988` <chr>, `1989` <chr>,
## #   `1990` <chr>, `1991` <chr>, `1992` <chr>, `1993` <chr>, `1994` <chr>,
## #   `1995` <chr>, `1996` <chr>, `1997` <chr>, `1998` <chr>, `1999` <chr>,
## #   `2000` <chr>, `2001` <chr>, `2002` <chr>, `2003` <chr>, `2004` <chr>,
## #   `2005` <chr>, `2006` <chr>, `2007` <chr>, `2008` <chr>, `2009` <chr>,
## #   `2010` <chr>, `2011` <chr>, `2012` <chr>
```

8. Are these data tidy? Why or why not, and, how do you know? Use the appropriate pivot function to tidy the data. Remove the NA's. Put the tidy data frame into a new object `fisheries_tidy`. 
## no there is a lot of NA, multiple values per cell, and the years should have one column.  

```r
fisheries3<-
fisheries2 %>% 
  pivot_longer(`1950`:`2012`,
               names_to= "year", 
               values_to= "catch", 
                values_drop_na= TRUE,
  )
fisheries3
```

```
## # A tibble: 376,771 x 10
##    country commname ISSCAAP_spgroup ISSCAAP_spgroup… ASFIS_spcode ASFIS_sciname
##    <fct>   <fct>              <dbl> <chr>            <chr>        <chr>        
##  1 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  2 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  3 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  4 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  5 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  6 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  7 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  8 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  9 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
## 10 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
## # … with 376,761 more rows, and 4 more variables: FAO_area <dbl>, unit <chr>,
## #   year <chr>, catch <chr>
```


```r
fisheries_tidy<-
fisheries3 %>% 
  transform(catch = str_split(catch, " ")) %>% 
                unnest(catch)
fisheries_tidy
```

```
## # A tibble: 411,421 x 10
##    country commname ISSCAAP_spgroup ISSCAAP_spgroup… ASFIS_spcode ASFIS_sciname
##    <fct>   <fct>              <dbl> <chr>            <chr>        <chr>        
##  1 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  2 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  3 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  4 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  5 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  6 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  7 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  8 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
##  9 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
## 10 Albania Angelsh…              38 Sharks, rays, c… 10903XXXXX   Squatinidae  
## # … with 411,411 more rows, and 4 more variables: FAO_area <dbl>, unit <chr>,
## #   year <chr>, catch <chr>
```

9. Refocus the data only to include country, ISSCAAP_spgroupname, ASFIS_spcode, ASFIS_sciname, year, and catch.

```r
fisheries_tidy2<-
fisheries_tidy %>% 
  select(country, ISSCAAP_spgroupname, ASFIS_spcode, ASFIS_sciname, year, catch)
fisheries_tidy2
```

```
## # A tibble: 411,421 x 6
##    country ISSCAAP_spgroupname     ASFIS_spcode ASFIS_sciname year  catch
##    <fct>   <chr>                   <chr>        <chr>         <chr> <chr>
##  1 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1995  0    
##  2 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1995  0    
##  3 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1996  53   
##  4 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1997  20   
##  5 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1998  31   
##  6 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1999  30   
##  7 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2000  30   
##  8 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2001  16   
##  9 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2002  79   
## 10 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2003  1    
## # … with 411,411 more rows
```

10. Re-check the classes of `fisheries_tidy2`. Notice that "catch" is shown as a character! This is a problem because we will want to treat it as a numeric. How will you deal with this?

```r
fisheries_tidy2$catch<- as.numeric(fisheries_tidy2$catch)
```

```
## Warning: NAs introduced by coercion
```

```r
fisheries_tidy2
```

```
## # A tibble: 411,421 x 6
##    country ISSCAAP_spgroupname     ASFIS_spcode ASFIS_sciname year  catch
##    <fct>   <chr>                   <chr>        <chr>         <chr> <dbl>
##  1 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1995      0
##  2 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1995      0
##  3 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1996     53
##  4 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1997     20
##  5 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1998     31
##  6 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1999     30
##  7 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2000     30
##  8 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2001     16
##  9 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2002     79
## 10 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2003      1
## # … with 411,411 more rows
```

11. Based on the ASFIS_spcode, how many distinct taxa were caught as part of these data?
## 1546

```r
fisheries_tidy2 %>% 
  summarise(n_taxa=n_distinct(ASFIS_sciname))
```

```
## # A tibble: 1 x 1
##   n_taxa
##    <int>
## 1   1546
```


12. Which country had the largest overall catch in the year 2000?

```r
fisheries_tidy2 %>% 
  select(year, country, catch) %>% 
  filter(year == "2000") %>% 
  arrange(desc(catch))
```

```
## # A tibble: 9,585 x 3
##    year  country                    catch
##    <chr> <fct>                      <dbl>
##  1 2000  Peru                     9575717
##  2 2000  China                    3419068
##  3 2000  Chile                    1700640
##  4 2000  Chile                    1234299
##  5 2000  Russian Federation       1215065
##  6 2000  China                    1203288
##  7 2000  United States of America 1182438
##  8 2000  China                    1102782
##  9 2000  China                    1041234
## 10 2000  Viet Nam                 1014945
## # … with 9,575 more rows
```
##peru had the largest overall catch

13. Which country caught the most sardines (_Sardina_) between the years 1990-2000?

```r
fisheries_tidy2 %>% 
  select(country, catch, year, ASFIS_sciname) %>% 
  filter(ASFIS_sciname == "Sardina pilchardus" & year>= 1990 & year<= 2000) %>% 
  group_by(country) %>% 
  summarise(catch= sum(catch, na.rm= TRUE)) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 37 x 2
##    country              catch
##    <fct>                <dbl>
##  1 Morocco            4785190
##  2 Spain              2056817
##  3 Russian Federation 1035139
##  4 Portugal            926318
##  5 Ukraine             784730
##  6 Algeria             631733
##  7 Italy               377907
##  8 Turkey              273565
##  9 France              263871
## 10 Denmark             242017
## # … with 27 more rows
```
## morocco
14. Which five countries caught the most cephalopods between 2008-2012?

```r
fisheries_tidy2 %>% 
  select(country, ISSCAAP_spgroupname, catch, year) %>% 
  filter(ISSCAAP_spgroupname == "Squids, cuttlefishes, octopuses" & year >= 2008 &year <= 2012) %>% 
  group_by(country) %>% 
summarise(catch= sum(catch, na.rm= TRUE)) %>% 
arrange(desc(catch))
```

```
## # A tibble: 122 x 2
##    country                    catch
##    <fct>                      <dbl>
##  1 China                    4785139
##  2 Peru                     2274232
##  3 Japan                    1644085
##  4 Korea, Republic of       1535454
##  5 Viet Nam                 1292000
##  6 Chile                     723186
##  7 Indonesia                 684567
##  8 United States of America  613400
##  9 Thailand                  603529
## 10 Taiwan Province of China  593638
## # … with 112 more rows
```
##China, Peru, Japan, Korea, and Viet Nam

15. Given the top five countries from question 12 above, which species was the highest catch total? The lowest?


```r
fisheries_tidy2 %>% 
  filter(ISSCAAP_spgroupname == "Squids, cuttlefishes, octopuses" & year>= 2008 & year <= 2012 & country == "China"| country == "Peru" | country == "Japan" | country == "Korea" | country == "Viet Nam") %>% 
  group_by(ASFIS_sciname) %>% 
  summarise(catch= sum(catch, na.rm= TRUE)) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 246 x 2
##    ASFIS_sciname               catch
##    <chr>                       <dbl>
##  1 Engraulis ringens       278401317
##  2 Osteichthyes             68449476
##  3 Sardinops melanostictus  62150527
##  4 Theragra chalcogramma    56940271
##  5 Scomber japonicus        43798362
##  6 Sardinops sagax          41879666
##  7 Todarodes pacificus      19707304
##  8 Engraulis japonicus      19546899
##  9 Katsuwonus pelamis       16832210
## 10 Cololabis saira          16511987
## # … with 236 more rows
```
##Highest catch is Engraulis Ringens, Lowest Catch is Trematomus spp

16. In some cases, the taxonomy of the fish being caught is unclear. Make a new data frame called `coastal_fish` that shows the taxonomic composition of "Miscellaneous coastal fishes" within the ISSCAAP_spgroupname column.


```r
coastal_fish<-
fisheries_tidy2 %>% 
  filter(ISSCAAP_spgroupname == "Miscellaneous coastal fishes")
```


17. Use the data to do at least one exploratory analysis of your choice. What can you learn?
##who catches the most miscellaneous coastal fishes?

```r
fisheries_tidy2 %>% 
  filter(ISSCAAP_spgroupname == "Miscellaneous coastal fishes") %>% 
  group_by(country) %>% 
  summarise(catch= sum(catch, na.rm= TRUE)) %>% 
  arrange(desc(catch))
```

```
## # A tibble: 150 x 2
##    country               catch
##    <fct>                 <dbl>
##  1 China              36961275
##  2 India              28060848
##  3 Denmark            24371336
##  4 Japan              22223753
##  5 Indonesia          18979007
##  6 Philippines        16273590
##  7 Korea, Republic of  9919627
##  8 Brazil              8918923
##  9 Thailand            7948087
## 10 Un. Sov. Soc. Rep.  7305555
## # … with 140 more rows
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
