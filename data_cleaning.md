Data cleaning
================

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(tidyr)

# Import dataset
df <-
  read.csv("Global YouTube Statistics.csv") |>
  janitor::clean_names()

# Check variable names 
variable_names <- names(df)
print(variable_names)
```

    ##  [1] "rank"                                "youtuber"                           
    ##  [3] "subscribers"                         "video_views"                        
    ##  [5] "category"                            "title"                              
    ##  [7] "uploads"                             "country"                            
    ##  [9] "abbreviation"                        "channel_type"                       
    ## [11] "video_views_rank"                    "country_rank"                       
    ## [13] "channel_type_rank"                   "video_views_for_the_last_30_days"   
    ## [15] "lowest_monthly_earnings"             "highest_monthly_earnings"           
    ## [17] "lowest_yearly_earnings"              "highest_yearly_earnings"            
    ## [19] "subscribers_for_last_30_days"        "created_year"                       
    ## [21] "created_month"                       "created_date"                       
    ## [23] "gross_tertiary_education_enrollment" "population"                         
    ## [25] "unemployment_rate"                   "urban_population"                   
    ## [27] "latitude"                            "longitude"

``` r
cleaned_df <- 
  df |>
  select(-youtuber,-title,-video_views_rank, -country_rank,-channel_type_rank, -created_month, -created_date, -gross_tertiary_education_enrollment, -unemployment_rate, -urban_population) |>
  rename(id = rank)

head(cleaned_df, 10)
```

    ##    id subscribers  video_views         category uploads       country
    ## 1   1   245000000 228000000000            Music   20082         India
    ## 2   2   170000000            0 Film & Animation       1 United States
    ## 3   3   166000000  28368841870    Entertainment     741 United States
    ## 4   4   162000000 164000000000        Education     966 United States
    ## 5   5   159000000 148000000000            Shows  116536         India
    ## 6   6   119000000            0              nan       0           nan
    ## 7   7   112000000  93247040539   People & Blogs    1111 United States
    ## 8   8   111000000  29058044447           Gaming    4716         Japan
    ## 9   9   106000000  90479060027   People & Blogs     493        Russia
    ## 10 10    98900000  77180169894    Entertainment     574 United States
    ##    abbreviation  channel_type video_views_for_the_last_30_days
    ## 1            IN         Music                       2258000000
    ## 2            US         Games                               12
    ## 3            US Entertainment                       1348000000
    ## 4            US     Education                       1975000000
    ## 5            IN Entertainment                       1824000000
    ## 6           nan         Music                              NaN
    ## 7            US Entertainment                        731674000
    ## 8            JP Entertainment                         39184000
    ## 9            RU        People                         48947000
    ## 10           US Entertainment                        580574000
    ##    lowest_monthly_earnings highest_monthly_earnings lowest_yearly_earnings
    ## 1                   564600                9.000e+06              6.800e+06
    ## 2                        0                5.000e-02              4.000e-02
    ## 3                   337000                5.400e+06              4.000e+06
    ## 4                   493800                7.900e+06              5.900e+06
    ## 5                   455900                7.300e+06              5.500e+06
    ## 6                        0                0.000e+00              0.000e+00
    ## 7                   182900                2.900e+06              2.200e+06
    ## 8                     9800                1.567e+05              1.176e+05
    ## 9                    12200                1.958e+05              1.468e+05
    ## 10                  145100                2.300e+06              1.700e+06
    ##    highest_yearly_earnings subscribers_for_last_30_days created_year population
    ## 1                1.084e+08                        2e+06         2006 1366417754
    ## 2                5.800e-01                          NaN         2006  328239523
    ## 3                6.470e+07                        8e+06         2012  328239523
    ## 4                9.480e+07                        1e+06         2006  328239523
    ## 5                8.750e+07                        1e+06         2006 1366417754
    ## 6                0.000e+00                          NaN         2013        NaN
    ## 7                3.510e+07                          NaN         2015  328239523
    ## 8                1.900e+06                          NaN         2010  126226568
    ## 9                2.300e+06                        1e+05         2016  144373535
    ## 10               2.790e+07                        6e+05         2018  328239523
    ##    latitude longitude
    ## 1  20.59368  78.96288
    ## 2  37.09024 -95.71289
    ## 3  37.09024 -95.71289
    ## 4  37.09024 -95.71289
    ## 5  20.59368  78.96288
    ## 6       NaN       NaN
    ## 7  37.09024 -95.71289
    ## 8  36.20482 138.25292
    ## 9  61.52401 105.31876
    ## 10 37.09024 -95.71289

``` r
# Save as new dataset
write.csv(cleaned_df, "cleaned_youtube_df.csv", row.names = FALSE)
```
