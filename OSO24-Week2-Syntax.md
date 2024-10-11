OSO24-Week2
================
Christine White
2024-10-11

## Data

**Dataset**:
<https://ldbase.org/projects/6238a896-f1cc-4cf9-9c52-b23fede10747>

**Citation**: Fuchs, L. S., Hamlett, C. L., Fuchs, D., Cho, E., Barnes,
M. A., Koponen, T., & Espinas, D. R. (2023). Comorbid Word Reading and
Math Computation Difficulty at Start of First Grade.
<https://doi.org/10.33009/ldbase.1691262928.78d5>

## Libraries

``` r
library(here) # here()
```

    ## here() starts at /Users/christinewhite/Library/CloudStorage/OneDrive-FloridaStateUniversity/New/School/6_LDbase/OSO Git/OSO-2024-Contributions

``` r
library(readxl) # read_excel() 
```

## Set-up

``` r
dat0 <- read_excel(here("OSO-Data/Comorbid Word Reading and Math Computation Difficulty at Start of First Grade.xlsx"))
```
