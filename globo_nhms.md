---
title: "globo_nhms"
output: 
  html_document: 
    keep_md: yes
---



# Prepare environment


```r
library(here)
```

```
## here() starts at /cloud/project
```

```r
library(tidyverse)
```

```
## ── Attaching packages ───────────────────────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.2.1     ✓ purrr   0.3.3
## ✓ tibble  2.1.3     ✓ dplyr   0.8.3
## ✓ tidyr   1.0.0     ✓ stringr 1.4.0
## ✓ readr   1.3.1     ✓ forcats 0.4.0
```

```
## ── Conflicts ──────────────────────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(haven)
library(usethis)
library(downloader)
```


# Read data



```r
globo <- read_sav("globo_nhms.sav")
globo <- globo %>% mutate_if(is.labelled, as_factor)
```

# Describe


```r
glimpse(globo)
```

```
## Observations: 29,460
## Variables: 26
## $ SurveyId               <chr> "06-08-020-0012-4-009-01-01", "12-19-065-0024-…
## $ ID                     <chr> "06-08-020-0012-4-009-01-01", "12-19-065-0024-…
## $ ebid                   <chr> "06080200012", "12190650024", "11040060063", "…
## $ State                  <fct> Pahang, Sabah & Labuan, Terengganu, Sabah & La…
## $ Strata                 <fct> Rural, Rural, Rural, Rural, Urban, Rural, Urba…
## $ NG_new                 <fct> Pahang, Sabah, Terengganu, Labuan, Perak, Perl…
## $ State_St               <fct> Pahang rural, Sabah rural, Terengganu rural, W…
## $ Sex                    <fct> Male, Male, Male, Male, Female, Male, Male, Ma…
## $ Ethnic3                <fct> Malay, Others Bumis, Malay, Others Bumis, Mala…
## $ Age                    <dbl> 114, 114, 100, 100, 99, 96, 96, 95, 95, 95, 93…
## $ Working_status         <fct> Retiree, Government Employee, Self-employed, N…
## $ Education              <fct> No formal education, Tertiary, No formal educa…
## $ Marital_status         <fct> Married, Never married, Married, Married, Wido…
## $ Agegroup               <fct> 75+, 75+, 75+, 75+, 75+, 75+, 75+, 75+, 75+, 7…
## $ ADW                    <dbl> 529.41474, 744.01365, 299.00903, 311.11111, 13…
## $ Weight_Final           <dbl> 775.05818, 473.34202, 325.00982, 25.00893, 135…
## $ total_cho              <fct> No, Yes, Yes, Yes, No, No, Yes, No, No, Yes, N…
## $ total_dm2              <fct> No, No, Yes, No, No, Yes, No, No, No, No, No, …
## $ Average_SYS            <dbl> 152.5, 120.0, 130.5, 121.0, 120.5, 143.5, 152.…
## $ Average_DYS            <dbl> 80.0, 60.0, 72.0, 60.5, 53.0, 84.5, 50.0, 71.0…
## $ Final_Hpt              <fct> Yes, No, No, No, No, Yes, Yes, No, No, Yes, No…
## $ Cigarette              <fct> No, No, No, No, No, Yes, No, No, No, No, No, N…
## $ Current_tobacco_smoker <fct> No, No, No, No, No, Yes, No, No, No, No, No, N…
## $ R4030                  <dbl> 4.60, 5.52, 6.54, 2.59, -9.00, 4.57, 5.42, 4.3…
## $ Berat                  <dbl> 65.4, 44.0, 50.6, NA, NA, NA, 49.8, NA, NA, NA…
## $ Tinggi                 <dbl> 167.1, 144.0, 163.2, NA, NA, NA, 140.5, NA, NA…
```

```r
summary(globo)
```

```
##    SurveyId              ID                ebid          
##  Length:29460       Length:29460       Length:29460      
##  Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character  
##                                                          
##                                                          
##                                                          
##                                                          
##             State         Strata           NG_new                State_St    
##  Selangor      : 4117   Urban:16880   Selangor: 4117   Selangor urban: 3201  
##  Sabah & Labuan: 2610   Rural:12580   Johor   : 2570   Johor urban   : 1703  
##  Johor         : 2570                 Sabah   : 2516   Sabah rural   : 1309  
##  Perak         : 1976                 Perak   : 1976   Sabah urban   : 1207  
##  Kelantan      : 1887                 Kelantan: 1887   Perak urban   : 1099  
##  Kedah         : 1880                 Kedah   : 1880   Kelantan rural: 1027  
##  (Other)       :14420                 (Other) :14514   (Other)       :19914  
##      Sex                Ethnic3           Age        
##  Male  :14225   Malay       :18845   Min.   :  0.00  
##  Female:15235   Chinese     : 4284   1st Qu.: 13.00  
##                 Indian      : 1993   Median : 30.00  
##                 Others Bumis: 2737   Mean   : 32.29  
##                 Others      : 1601   3rd Qu.: 50.00  
##                                      Max.   :114.00  
##                                                      
##              Working_status                Education    
##  Private            : 6206   No formal education: 1995  
##  Self-employed      : 3892   Primary            : 8611  
##  Homemaker          : 3320   Secondary          :10354  
##  Student            : 2668   Tertiary           : 4403  
##  Government Employee: 1913   Unclassified       : 1043  
##  (Other)            : 1100   NA's               : 3054  
##  NA's               :10361                              
##                 Marital_status     Agegroup          ADW         
##  Never married         : 6687   <= 4   : 2689   Min.   :  60.62  
##  Married               :13860   5 - 9  : 2688   1st Qu.: 389.89  
##  Widow/Widower/Divorcee: 1941   10 - 14: 2638   Median : 744.01  
##  NA's                  : 6972   15 - 19: 2291   Mean   : 817.48  
##                                 25 - 29: 2176   3rd Qu.:1291.88  
##                                 30 - 34: 2096   Max.   :1613.52  
##                                 (Other):14882                    
##   Weight_Final       total_cho    total_dm2     Average_SYS     Average_DYS    
##  Min.   :    8.327   No  : 9421   No  :15706   Min.   : -9.0   Min.   : -9.00  
##  1st Qu.:  420.012   Yes :10514   Yes : 4229   1st Qu.:116.0   1st Qu.: 71.00  
##  Median :  838.638   NA's: 9525   NA's: 9525   Median :127.0   Median : 78.50  
##  Mean   :  997.088                             Mean   :125.4   Mean   : 76.01  
##  3rd Qu.: 1409.525                             3rd Qu.:140.0   3rd Qu.: 85.00  
##  Max.   :23192.857                             Max.   :250.0   Max.   :169.00  
##                                                NA's   :9524    NA's   :9524    
##  Final_Hpt    Cigarette    Current_tobacco_smoker     R4030      
##  No  :12711   Yes : 4399   Yes : 4477             Min.   :-9.00  
##  Yes : 7225   No  :17016   No  :16938             1st Qu.: 4.20  
##  NA's: 9524   NA's: 8045   NA's: 8045             Median : 5.11  
##                                                   Mean   : 4.28  
##                                                   3rd Qu.: 6.07  
##                                                   Max.   :10.40  
##                                                   NA's   :9578   
##      Berat            Tinggi     
##  Min.   : 25.70   Min.   : 73.2  
##  1st Qu.: 54.90   1st Qu.:152.9  
##  Median : 63.85   Median :159.0  
##  Mean   : 65.66   Mean   :159.2  
##  3rd Qu.: 74.40   3rd Qu.:165.6  
##  Max.   :151.60   Max.   :210.5  
##  NA's   :10930    NA's   :10929
```

