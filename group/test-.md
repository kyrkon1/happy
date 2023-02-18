---
title: "Test"
output: 
  html_document: 
    keep_md: yes
date: "2023-02-16"
---



```r
#install.packages("stringr")
```


```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.1 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.2.1      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(naniar)
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
library(here)
```

```
## here() starts at /Users/harikakovvuri/Desktop/happy-main/group
```

```r
library(stringr)
```



```r
happy <- readr::read_csv("data/2022.csv")
```

```
## Rows: 147 Columns: 12
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (8): Country, Dystopia (1.83) + residual, Explained by: GDP per capita, ...
## dbl (1): RANK
## num (3): Happiness score, Whisker-high, Whisker-low
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

#Clean Up of Data

```r
happy
```

```
## # A tibble: 147 × 12
##     RANK Country Happi…¹ Whisk…² Whisk…³ Dysto…⁴ Expla…⁵ Expla…⁶ Expla…⁷ Expla…⁸
##    <dbl> <chr>     <dbl>   <dbl>   <dbl> <chr>   <chr>   <chr>   <chr>   <chr>  
##  1     1 Finland    7821    7886    7756 2,518   1,892   1,258   0,775   0,736  
##  2     2 Denmark    7636    7710    7563 2,226   1,953   1,243   0,777   0,719  
##  3     3 Iceland    7557    7651    7464 2,320   1,936   1,320   0,803   0,718  
##  4     4 Switze…    7512    7586    7437 2,153   2,026   1,226   0,822   0,677  
##  5     5 Nether…    7415    7471    7359 2,137   1,945   1,206   0,787   0,651  
##  6     6 Luxemb…    7404    7501    7307 2,042   2,209   1,155   0,790   0,700  
##  7     7 Sweden     7384    7454    7315 2,003   1,920   1,204   0,803   0,724  
##  8     8 Norway     7365    7440    7290 1,925   1,997   1,239   0,786   0,728  
##  9     9 Israel     7364    7426    7301 2,634   1,826   1,221   0,818   0,568  
## 10    10 New Ze…    7200    7279    7120 1,954   1,852   1,235   0,752   0,680  
## # … with 137 more rows, 2 more variables: `Explained by: Generosity` <chr>,
## #   `Explained by: Perceptions of corruption` <chr>, and abbreviated variable
## #   names ¹​`Happiness score`, ²​`Whisker-high`, ³​`Whisker-low`,
## #   ⁴​`Dystopia (1.83) + residual`, ⁵​`Explained by: GDP per capita`,
## #   ⁶​`Explained by: Social support`, ⁷​`Explained by: Healthy life expectancy`,
## #   ⁸​`Explained by: Freedom to make life choices`
```

clean names

```r
happy <- janitor::clean_names(happy)
```

convert euro commas to points


```r
happy %>% 
  mutate_all(~str_replace_all(.,",","."))
```

```
## # A tibble: 147 × 12
##    rank  country happi…¹ whisk…² whisk…³ dysto…⁴ expla…⁵ expla…⁶ expla…⁷ expla…⁸
##    <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
##  1 1     Finland 7821    7886    7756    2.518   1.892   1.258   0.775   0.736  
##  2 2     Denmark 7636    7710    7563    2.226   1.953   1.243   0.777   0.719  
##  3 3     Iceland 7557    7651    7464    2.320   1.936   1.320   0.803   0.718  
##  4 4     Switze… 7512    7586    7437    2.153   2.026   1.226   0.822   0.677  
##  5 5     Nether… 7415    7471    7359    2.137   1.945   1.206   0.787   0.651  
##  6 6     Luxemb… 7404    7501    7307    2.042   2.209   1.155   0.790   0.700  
##  7 7     Sweden  7384    7454    7315    2.003   1.920   1.204   0.803   0.724  
##  8 8     Norway  7365    7440    7290    1.925   1.997   1.239   0.786   0.728  
##  9 9     Israel  7364    7426    7301    2.634   1.826   1.221   0.818   0.568  
## 10 10    New Ze… 7200    7279    7120    1.954   1.852   1.235   0.752   0.680  
## # … with 137 more rows, 2 more variables: explained_by_generosity <chr>,
## #   explained_by_perceptions_of_corruption <chr>, and abbreviated variable
## #   names ¹​happiness_score, ²​whisker_high, ³​whisker_low,
## #   ⁴​dystopia_1_83_residual, ⁵​explained_by_gdp_per_capita,
## #   ⁶​explained_by_social_support, ⁷​explained_by_healthy_life_expectancy,
## #   ⁸​explained_by_freedom_to_make_life_choices
```

insert decimal points back into data




#Structural Analysis


```r
names(happy)
```

```
##  [1] "rank"                                     
##  [2] "country"                                  
##  [3] "happiness_score"                          
##  [4] "whisker_high"                             
##  [5] "whisker_low"                              
##  [6] "dystopia_1_83_residual"                   
##  [7] "explained_by_gdp_per_capita"              
##  [8] "explained_by_social_support"              
##  [9] "explained_by_healthy_life_expectancy"     
## [10] "explained_by_freedom_to_make_life_choices"
## [11] "explained_by_generosity"                  
## [12] "explained_by_perceptions_of_corruption"
```


```r
glimpse(happy)
```

```
## Rows: 147
## Columns: 12
## $ rank                                      <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 1…
## $ country                                   <chr> "Finland", "Denmark", "Icela…
## $ happiness_score                           <dbl> 7821, 7636, 7557, 7512, 7415…
## $ whisker_high                              <dbl> 7886, 7710, 7651, 7586, 7471…
## $ whisker_low                               <dbl> 7756, 7563, 7464, 7437, 7359…
## $ dystopia_1_83_residual                    <chr> "2,518", "2,226", "2,320", "…
## $ explained_by_gdp_per_capita               <chr> "1,892", "1,953", "1,936", "…
## $ explained_by_social_support               <chr> "1,258", "1,243", "1,320", "…
## $ explained_by_healthy_life_expectancy      <chr> "0,775", "0,777", "0,803", "…
## $ explained_by_freedom_to_make_life_choices <chr> "0,736", "0,719", "0,718", "…
## $ explained_by_generosity                   <chr> "0,109", "0,188", "0,270", "…
## $ explained_by_perceptions_of_corruption    <chr> "0,534", "0,532", "0,191", "…
```






