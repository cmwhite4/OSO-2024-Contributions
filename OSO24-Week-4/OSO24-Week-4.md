OSO24-Week-4
================
Christine White
2024-10-28

## Dataset

Ceviren, A. B., & Logan, J. A. (2023). Data Sharing Beliefs and
Attitudes Data.
<http://ldbase.org/datasets/14d882ca-85d8-44dd-821d-b39121e3fb53>

## Setup

## Libraries

``` r
library(tidyverse)
library(here)
library(formattable)
```

## Data Import

``` r
dat0 <- read.csv(here("OSO-Data/data_sharing_data.csv")) |>
  select(-1) # Remove extra column "X"
```

## Data Preparation

``` r
# Subset to relevant columns 
dat1 <- dat0 |> select(ds.agreementfinal, contains("5d")) |>
  drop_na() |>
  group_by(ds.agreementfinal) |> 
  summarise(`Benefits Science` = round(sum(ds.Q5d_1 > 3)/n(), 2),
            `Good for Career` = round(sum(ds.Q5d_3 > 3)/n(), 2),
            `More Citations` = round(sum(ds.Q5d_7 > 3)/n(), 2),
            `IRB Concerns` = round(sum(ds.Q5d_2 > 3)/n(), 2),
            `Participant Risk` = round(sum(ds.Q5d_5 > 3)/n(), 2),
            `Data Scooping` = round(sum(ds.Q5d_6 > 3)/n(), 2),
            `Time or Resources` = round(sum(ds.Q5d_11 > 3)/n(), 2)) |>
  mutate(Group = dplyr::case_match(ds.agreementfinal, 
                      1 ~ "Believer",
                      0 ~ "Skeptic")) |>
  select(-ds.agreementfinal) |>
  select(Group, everything())
```

## Plot (Table)

``` r
library(formattable)
formattable(dat1, 
            caption = "What proportion of surveyed education researchers (n = 178) agreed to any extent with the following benefits of (green) and barriers to (blue) data sharing?",
            align = c("l", rep("c", NCOL(dat1)-1)),
            list(`Group` = formatter("span", style = ~ style(color = "grey", 
                                                             font.weight = "bold")),
                 area(col = 2:4) ~ color_tile("#e5ede0", "#a1c18e"),
                 area(col = 5:8) ~ color_tile("#bad5e2", "#61a1c0")))
```

<table class="table table-condensed">
<caption>
What proportion of surveyed education researchers (n = 178) agreed to
any extent with the following benefits of (green) and barriers to (blue)
data sharing?
</caption>
<thead>
<tr>
<th style="text-align:left;">
Group
</th>
<th style="text-align:center;">
Benefits Science
</th>
<th style="text-align:center;">
Good for Career
</th>
<th style="text-align:center;">
More Citations
</th>
<th style="text-align:center;">
IRB Concerns
</th>
<th style="text-align:center;">
Participant Risk
</th>
<th style="text-align:center;">
Data Scooping
</th>
<th style="text-align:center;">
Time or Resources
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
<span style="color: grey; font-weight: bold">Skeptic </span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #a7c595">0.91</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #e5ede0">0.02</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #c5d8ba">0.47</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #61a1c0">0.77</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #9cc3d6">0.49</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #85b6cd">0.60</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #80b3cc">0.62</span>
</td>
</tr>
<tr>
<td style="text-align:left;">
<span style="color: grey; font-weight: bold">Believer</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #a1c18e">1.00</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #a1c18e">1.00</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #aec99e">0.80</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #95bfd4">0.52</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bad5e2">0.35</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #bad5e2">0.35</span>
</td>
<td style="text-align:center;">
<span style="display: block; padding: 0 4px; border-radius: 4px; background-color: #8dbbd1">0.56</span>
</td>
</tr>
</tbody>
</table>
