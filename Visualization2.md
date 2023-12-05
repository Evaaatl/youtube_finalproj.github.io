Visulization Part 2
================
You Wu
2023-12-05

Load necessary packages.

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(plotly)
```

    ## 
    ## Attaching package: 'plotly'
    ## 
    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     last_plot
    ## 
    ## The following object is masked from 'package:stats':
    ## 
    ##     filter
    ## 
    ## The following object is masked from 'package:graphics':
    ## 
    ##     layout

Read the dataset and drop `NA` vlaues.

``` r
youtube_df <- read_csv("Data/cleaned_youtube_df.csv")|>
  janitor::clean_names()|>
  drop_na()
```

    ## Rows: 995 Columns: 18
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (4): category, country, abbreviation, channel_type
    ## dbl (14): id, subscribers, video_views, uploads, video_views_for_the_last_30...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
summary(youtube_df)
```

    ##        id         subscribers         video_views          category        
    ##  Min.   :  1.0   Min.   : 12300000   Min.   :2.634e+03   Length:589        
    ##  1st Qu.:213.0   1st Qu.: 14700000   1st Qu.:4.910e+09   Class :character  
    ##  Median :454.0   Median : 18600000   Median :8.761e+09   Mode  :character  
    ##  Mean   :471.2   Mean   : 24264516   Mean   :1.280e+10                     
    ##  3rd Qu.:723.0   3rd Qu.: 26400000   3rd Qu.:1.507e+10                     
    ##  Max.   :995.0   Max.   :245000000   Max.   :2.280e+11                     
    ##     uploads         country          abbreviation       channel_type      
    ##  Min.   :     1   Length:589         Length:589         Length:589        
    ##  1st Qu.:   433   Class :character   Class :character   Class :character  
    ##  Median :  1189   Mode  :character   Mode  :character   Mode  :character  
    ##  Mean   : 13945                                                           
    ##  3rd Qu.:  3882                                                           
    ##  Max.   :301308                                                           
    ##  video_views_for_the_last_30_days lowest_monthly_earnings
    ##  Min.   :3.000e+00                Min.   :     0         
    ##  1st Qu.:4.845e+07                1st Qu.: 11500         
    ##  Median :1.143e+08                Median : 28200         
    ##  Mean   :2.446e+08                Mean   : 54260         
    ##  3rd Qu.:2.441e+08                3rd Qu.: 59000         
    ##  Max.   :6.589e+09                Max.   :850900         
    ##  highest_monthly_earnings lowest_yearly_earnings highest_yearly_earnings
    ##  Min.   :       0         Min.   :       0       Min.   :        0      
    ##  1st Qu.:  183200         1st Qu.:  137400       1st Qu.:  2200000      
    ##  Median :  451100         Median :  338300       Median :  5400000      
    ##  Mean   :  867499         Mean   :  650618       Mean   : 10417717      
    ##  3rd Qu.:  944000         3rd Qu.:  708000       3rd Qu.: 11300000      
    ##  Max.   :13600000         Max.   :10200000       Max.   :163400000      
    ##  subscribers_for_last_30_days  created_year    population       
    ##  Min.   :      1              Min.   :1970   Min.   :2.025e+05  
    ##  1st Qu.: 100000              1st Qu.:2010   1st Qu.:1.081e+08  
    ##  Median : 200000              Median :2013   Median :3.282e+08  
    ##  Mean   : 356695              Mean   :2013   Mean   :4.906e+08  
    ##  3rd Qu.: 400000              3rd Qu.:2016   3rd Qu.:3.282e+08  
    ##  Max.   :8000000              Max.   :2022   Max.   :1.398e+09  
    ##     latitude        longitude       
    ##  Min.   :-38.42   Min.   :-172.105  
    ##  1st Qu.: 20.59   1st Qu.: -95.713  
    ##  Median : 30.59   Median :  -3.436  
    ##  Mean   : 26.21   Mean   :  -6.254  
    ##  3rd Qu.: 37.09   3rd Qu.:  78.963  
    ##  Max.   : 61.52   Max.   : 138.253
