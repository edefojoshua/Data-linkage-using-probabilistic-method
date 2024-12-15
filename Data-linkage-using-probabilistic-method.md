Data linkage using probabilistic method
================
Joshua Edefo
2024-12-15

Step 1: Install and load the necessary packages Libraries

``` r
library(usethis)
```

    ## Warning: package 'usethis' was built under R version 4.3.2

``` r
# install.packages("RecordLinkage")
library(RecordLinkage)
```

    ## Warning: package 'RecordLinkage' was built under R version 4.3.3

    ## Warning: package 'DBI' was built under R version 4.3.2

    ## Warning: package 'RSQLite' was built under R version 4.3.3

    ## Warning: package 'ff' was built under R version 4.3.3

Other steps

``` r
# Step 2: Prepare Your Data

# Example data frames
df1 <- data.frame(
  id = 1:3,
  name = c("John Doe", "Jane Smith", "Alice Johnson"),
  dob = as.Date(c("1980-01-01", "1990-05-15", "1985-07-30")),
  postcode = c("12345", "23456", "34567")
)

df2 <- data.frame(
  id = 4:6,
  name = c("Jon Doe", "Jane Smyth", "Alicia Johnson"),
  dob = as.Date(c("1980-01-01", "1990-05-15", "1985-07-30")),
  postcode = c("12345", "23456", "34567")
)

# Step 3: Create a Record Linkage Object
# Create a RecordLinkage object
linkage <- compare.linkage(df1, df2, 
                           blockfld = c("dob", "postcode"), 
                           strcmp = c("name"))

# Step 4: Perform Probabilistic Linkage

# Calculate weights using the Expectation-Maximization algorithm
linkage <- emWeights(linkage)
```

``` r
#Step 5: Classify Matches
#Classify the matches based on the calculated weights.
matches <- getPairs(linkage)

matches_filtered <- matches[matches$prob >= 0.75 & matches$prob <= 0.85, ]

# View the matched pairs
print(matches_filtered)
```

    ## [1] id       id       name     dob      postcode Weight  
    ## <0 rows> (or 0-length row.names)

session information

``` r
sessionInfo()
```

    ## R version 4.3.1 (2023-06-16 ucrt)
    ## Platform: x86_64-w64-mingw32/x64 (64-bit)
    ## Running under: Windows 11 x64 (build 22631)
    ## 
    ## Matrix products: default
    ## 
    ## 
    ## locale:
    ## [1] LC_COLLATE=English_United Kingdom.utf8 
    ## [2] LC_CTYPE=English_United Kingdom.utf8   
    ## [3] LC_MONETARY=English_United Kingdom.utf8
    ## [4] LC_NUMERIC=C                           
    ## [5] LC_TIME=English_United Kingdom.utf8    
    ## 
    ## time zone: Europe/London
    ## tzcode source: internal
    ## 
    ## attached base packages:
    ## [1] stats     graphics  grDevices utils     datasets  methods   base     
    ## 
    ## other attached packages:
    ## [1] RecordLinkage_0.4-12.4 ff_4.5.0               bit_4.0.5             
    ## [4] RSQLite_2.3.9          DBI_1.2.0              usethis_2.2.2         
    ## 
    ## loaded via a namespace (and not attached):
    ##  [1] Matrix_1.6-1.1      future.apply_1.11.1 compiler_4.3.1     
    ##  [4] Rcpp_1.0.11         rpart_4.1.19        blob_1.2.4         
    ##  [7] parallel_4.3.1      ada_2.0-5           globals_0.16.2     
    ## [10] splines_4.3.1       yaml_2.3.7          fastmap_1.2.0      
    ## [13] lattice_0.21-8      prodlim_2023.08.28  knitr_1.44         
    ## [16] MASS_7.3-60         future_1.33.1       evd_2.3-7.1        
    ## [19] nnet_7.3-19         rlang_1.1.1         cachem_1.1.0       
    ## [22] xfun_0.40           fs_1.6.3            bit64_4.0.5        
    ## [25] memoise_2.0.1       cli_3.6.1           magrittr_2.0.3     
    ## [28] class_7.3-22        digest_0.6.33       grid_4.3.1         
    ## [31] ipred_0.9-14        xtable_1.8-4        rstudioapi_0.15.0  
    ## [34] lifecycle_1.0.3     lava_1.7.3          vctrs_0.6.5        
    ## [37] proxy_0.4-27        evaluate_0.21       glue_1.6.2         
    ## [40] data.table_1.14.8   listenv_0.9.0       codetools_0.2-19   
    ## [43] survival_3.7-0      parallelly_1.36.0   e1071_1.7-14       
    ## [46] rmarkdown_2.25      purrr_1.0.2         tools_4.3.1        
    ## [49] htmltools_0.5.8.1
