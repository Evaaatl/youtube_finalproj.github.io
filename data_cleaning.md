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
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ forcats   1.0.0     ✔ readr     2.1.4
    ## ✔ ggplot2   3.4.3     ✔ stringr   1.5.0
    ## ✔ lubridate 1.9.2     ✔ tibble    3.2.1
    ## ✔ purrr     1.0.2

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
# Import dataset
df <-
  read_csv("Data/Global YouTube Statistics.csv") |>
  janitor::clean_names()
```

    ## Rows: 995 Columns: 28
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (7): Youtuber, category, Title, Country, Abbreviation, channel_type, cr...
    ## dbl (21): rank, subscribers, video views, uploads, video_views_rank, country...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# Check variable names 
variable_names <- names(df)
print(variable_names)
```

    ##  [1] "rank"                                       
    ##  [2] "youtuber"                                   
    ##  [3] "subscribers"                                
    ##  [4] "video_views"                                
    ##  [5] "category"                                   
    ##  [6] "title"                                      
    ##  [7] "uploads"                                    
    ##  [8] "country"                                    
    ##  [9] "abbreviation"                               
    ## [10] "channel_type"                               
    ## [11] "video_views_rank"                           
    ## [12] "country_rank"                               
    ## [13] "channel_type_rank"                          
    ## [14] "video_views_for_the_last_30_days"           
    ## [15] "lowest_monthly_earnings"                    
    ## [16] "highest_monthly_earnings"                   
    ## [17] "lowest_yearly_earnings"                     
    ## [18] "highest_yearly_earnings"                    
    ## [19] "subscribers_for_last_30_days"               
    ## [20] "created_year"                               
    ## [21] "created_month"                              
    ## [22] "created_date"                               
    ## [23] "gross_tertiary_education_enrollment_percent"
    ## [24] "population"                                 
    ## [25] "unemployment_rate"                          
    ## [26] "urban_population"                           
    ## [27] "latitude"                                   
    ## [28] "longitude"

``` r
cleaned_df <- df |>
  select(-youtuber,-title,-video_views_rank, -country_rank,-channel_type_rank, -created_month, -created_date, -gross_tertiary_education_enrollment_percent, -unemployment_rate, -urban_population) |> 
  rename(id = rank)

head(cleaned_df, 10)
```

    ## # A tibble: 10 × 18
    ##       id subscribers  video_views category         uploads country  abbreviation
    ##    <dbl>       <dbl>        <dbl> <chr>              <dbl> <chr>    <chr>       
    ##  1     1   245000000 228000000000 Music              20082 India    IN          
    ##  2     2   170000000            0 Film & Animation       1 United … US          
    ##  3     3   166000000  28368841870 Entertainment        741 United … US          
    ##  4     4   162000000 164000000000 Education            966 United … US          
    ##  5     5   159000000 148000000000 Shows             116536 India    IN          
    ##  6     6   119000000            0 nan                    0 nan      nan         
    ##  7     7   112000000  93247040539 People & Blogs      1111 United … US          
    ##  8     8   111000000  29058044447 Gaming              4716 Japan    JP          
    ##  9     9   106000000  90479060027 People & Blogs       493 Russia   RU          
    ## 10    10    98900000  77180169894 Entertainment        574 United … US          
    ## # ℹ 11 more variables: channel_type <chr>,
    ## #   video_views_for_the_last_30_days <dbl>, lowest_monthly_earnings <dbl>,
    ## #   highest_monthly_earnings <dbl>, lowest_yearly_earnings <dbl>,
    ## #   highest_yearly_earnings <dbl>, subscribers_for_last_30_days <dbl>,
    ## #   created_year <dbl>, population <dbl>, latitude <dbl>, longitude <dbl>

``` r
# Save as a new dataset
write_csv(cleaned_df, path = "./Data/cleaned_youtube_df.csv")
```

    ## Warning: The `path` argument of `write_csv()` is deprecated as of readr 1.4.0.
    ## ℹ Please use the `file` argument instead.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
    ## generated.

``` r
read_csv("Data/cleaned_youtube_df.csv")
```

    ## Rows: 995 Columns: 18
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (4): category, country, abbreviation, channel_type
    ## dbl (14): id, subscribers, video_views, uploads, video_views_for_the_last_30...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## # A tibble: 995 × 18
    ##       id subscribers  video_views category         uploads country  abbreviation
    ##    <dbl>       <dbl>        <dbl> <chr>              <dbl> <chr>    <chr>       
    ##  1     1   245000000 228000000000 Music              20082 India    IN          
    ##  2     2   170000000            0 Film & Animation       1 United … US          
    ##  3     3   166000000  28368841870 Entertainment        741 United … US          
    ##  4     4   162000000 164000000000 Education            966 United … US          
    ##  5     5   159000000 148000000000 Shows             116536 India    IN          
    ##  6     6   119000000            0 nan                    0 nan      nan         
    ##  7     7   112000000  93247040539 People & Blogs      1111 United … US          
    ##  8     8   111000000  29058044447 Gaming              4716 Japan    JP          
    ##  9     9   106000000  90479060027 People & Blogs       493 Russia   RU          
    ## 10    10    98900000  77180169894 Entertainment        574 United … US          
    ## # ℹ 985 more rows
    ## # ℹ 11 more variables: channel_type <chr>,
    ## #   video_views_for_the_last_30_days <dbl>, lowest_monthly_earnings <dbl>,
    ## #   highest_monthly_earnings <dbl>, lowest_yearly_earnings <dbl>,
    ## #   highest_yearly_earnings <dbl>, subscribers_for_last_30_days <dbl>,
    ## #   created_year <dbl>, population <dbl>, latitude <dbl>, longitude <dbl>

``` r
table(cleaned_df$category)
```

    ## 
    ##      Autos & Vehicles                Comedy             Education 
    ##                     2                    69                    45 
    ##         Entertainment      Film & Animation                Gaming 
    ##                   241                    46                    94 
    ##         Howto & Style                Movies                 Music 
    ##                    40                     2                   202 
    ##                   nan       News & Politics Nonprofits & Activism 
    ##                    46                    26                     2 
    ##        People & Blogs        Pets & Animals  Science & Technology 
    ##                   132                     4                    17 
    ##                 Shows                Sports              Trailers 
    ##                    13                    11                     2 
    ##       Travel & Events 
    ##                     1

``` r
table(cleaned_df$channel_type)
```

    ## 
    ##       Animals         Autos        Comedy     Education Entertainment 
    ##             3             3            51            49           304 
    ##          Film         Games         Howto         Music           nan 
    ##            42            98            36           216            30 
    ##          News     Nonprofit        People        Sports          Tech 
    ##            30             2           101            13            17

``` r
table(cleaned_df$country)
```

    ## 
    ##          Afghanistan              Andorra            Argentina 
    ##                    1                    1                   13 
    ##            Australia           Bangladesh             Barbados 
    ##                    9                    1                    1 
    ##               Brazil               Canada                Chile 
    ##                   62                   15                    3 
    ##                China             Colombia                 Cuba 
    ##                    1                   11                    1 
    ##              Ecuador                Egypt          El Salvador 
    ##                    2                    2                    1 
    ##              Finland               France              Germany 
    ##                    1                    5                    6 
    ##                India            Indonesia                 Iraq 
    ##                  168                   28                    2 
    ##                Italy                Japan               Jordan 
    ##                    2                    5                    3 
    ##               Kuwait               Latvia             Malaysia 
    ##                    1                    1                    1 
    ##               Mexico              Morocco                  nan 
    ##                   33                    1                  122 
    ##          Netherlands             Pakistan                 Peru 
    ##                    3                    6                    1 
    ##          Philippines               Russia                Samoa 
    ##                   12                   16                    1 
    ##         Saudi Arabia            Singapore          South Korea 
    ##                    9                    3                   17 
    ##                Spain               Sweden          Switzerland 
    ##                   22                    4                    1 
    ##             Thailand               Turkey              Ukraine 
    ##                   18                    4                    8 
    ## United Arab Emirates       United Kingdom        United States 
    ##                    7                   43                  313 
    ##            Venezuela              Vietnam 
    ##                    1                    3
