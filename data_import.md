Data Import
================

This document will show how to import data.

## Import the FAS Litters CSV

Import the dataset and clean the names.

``` r
litters_df = read_csv("data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df)
```

## Look at the dataset

``` r
litters_df
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>           <chr>      <chr>             <dbl>           <dbl>
    ##  1 Con7  #85             19.7       34.7                 20               3
    ##  2 Con7  #1/2/95/2       27         42                   19               8
    ##  3 Con7  #5/5/3/83/3-3   26         41.4                 19               6
    ##  4 Con7  #5/4/2/95/2     28.5       44.1                 19               5
    ##  5 Con7  #4/2/95/3-3     <NA>       <NA>                 20               6
    ##  6 Con7  #2/2/95/3-2     <NA>       <NA>                 20               6
    ##  7 Con7  #1/5/3/83/3-3/2 <NA>       <NA>                 20               9
    ##  8 Con8  #3/83/3-3       <NA>       <NA>                 20               9
    ##  9 Con8  #2/95/3         <NA>       <NA>                 20               8
    ## 10 Con8  #3/5/2/2/95     28.5       <NA>                 20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Con7  #85           19.7       34.7                 20               3
    ## 2 Con7  #1/2/95/2     27         42                   19               8
    ## 3 Con7  #5/5/3/83/3-3 26         41.4                 19               6
    ## 4 Con7  #5/4/2/95/2   28.5       44.1                 19               5
    ## 5 Con7  #4/2/95/3-3   <NA>       <NA>                 20               6
    ## 6 Con7  #2/2/95/3-2   <NA>       <NA>                 20               6
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
tail(litters_df, 10)
```

    ## # A tibble: 10 × 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ##  1 Mod8  #7/110/3-2    27.5       46                   19               8
    ##  2 Mod8  #2/95/2       28.5       44.5                 20               9
    ##  3 Mod8  #82/4         33.4       52.7                 20               8
    ##  4 Low8  #53           21.8       37.2                 20               8
    ##  5 Low8  #79           25.4       43.8                 19               8
    ##  6 Low8  #100          20         39.2                 20               8
    ##  7 Low8  #4/84         21.8       35.2                 20               4
    ##  8 Low8  #108          25.6       47.5                 20               8
    ##  9 Low8  #99           23.5       39                   20               6
    ## 10 Low8  #110          25.5       42.7                 20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
view(litters_df)
```

\#Import FAS Pups

Use relative paths.

``` r
pups_df = read_csv("data/FAS_pups.csv")
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Litter Number, PD ears
    ## dbl (4): Sex, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
pups_df = janitor::clean_names(pups_df)
```

Use absolute path. Caution: If you move the folder, the code below will
not work. Use relative paths instead.

``` r
pups_df = read_csv("/Users/mahdi/Desktop/data_wrangling_I/data/FAS_pups.csv")
```

## Look at read_csv options

col_names and skip rows

Skip = will be helpful if you don’t want to include first couple of rows

``` r
litters_df = 
  read_csv(
    file = "data/FAS_litters.csv",
    col_names = FALSE,
    skip = 1
  )
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): X1, X2, X3, X4
    ## dbl (4): X5, X6, X7, X8
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

What about missing data

using na = to correct missing variables

``` r
litters_df =
  read_csv(
    file = "data/FAS_litters.csv",
    na = c("NA", "", ".")
  )
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df)
```

What if we code `group` as a factor variable?

``` r
litters_df = 
  read_csv(
    file = "data/FAS_litters.csv",
    na = c("NA", "", "."),
    col_types = cols(
      Group = col_factor()
    )
  )
```

## Import an excel file

Import MLB 2011 summary data using read_excel, sheet, range.

``` r
mlb_df = read_excel("data/mlb11.xlsx", sheet = "mlb11")
```

## Import SAS data

``` r
pulse_df = read_sas("data/public_pulse_data.sas7bdat")
```

## Never use read.csv()

Use `read_csv()`

``` r
litters_df = read.csv("data/FAS_litters.csv")
```

Never do this either: `$` are generally bad

``` r
litters_df$L
```

    ##  [1] "#85"             "#1/2/95/2"       "#5/5/3/83/3-3"   "#5/4/2/95/2"    
    ##  [5] "#4/2/95/3-3"     "#2/2/95/3-2"     "#1/5/3/83/3-3/2" "#3/83/3-3"      
    ##  [9] "#2/95/3"         "#3/5/2/2/95"     "#5/4/3/83/3"     "#1/6/2/2/95-2"  
    ## [13] "#3/5/3/83/3-3-2" "#2/2/95/2"       "#3/6/2/2/95-3"   "#59"            
    ## [17] "#103"            "#1/82/3-2"       "#3/83/3-2"       "#2/95/2-2"      
    ## [21] "#3/82/3-2"       "#4/2/95/2"       "#5/3/83/5-2"     "#8/110/3-2"     
    ## [25] "#106"            "#94/2"           "#62"             "#84/2"          
    ## [29] "#107"            "#85/2"           "#98"             "#102"           
    ## [33] "#101"            "#111"            "#112"            "#97"            
    ## [37] "#5/93"           "#5/93/2"         "#7/82-3-2"       "#7/110/3-2"     
    ## [41] "#2/95/2"         "#82/4"           "#53"             "#79"            
    ## [45] "#100"            "#4/84"           "#108"            "#99"            
    ## [49] "#110"
