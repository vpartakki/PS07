R Code from Data Science Projects
================

## Data visualizations for SDS 192

This is a document containing two data visualizations I created for my
data science class!

## Number of campaign stops Clinton and Trump made each week leading up to the 2016 election.

Code and Visualization:

``` r
library(ggplot2)
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
library(fivethirtyeight)
```

    ## Some larger datasets need to be installed separately, like senators and
    ## house_district_forecast. To install these, we recommend you install the
    ## fivethirtyeightdata package by running:
    ## install.packages('fivethirtyeightdata', repos =
    ## 'https://fivethirtyeightdata.github.io/drat/', type = 'source')

``` r
library(moderndive)
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
weekly_campaign_stops <- pres_2016_trail %>% 
  mutate(week = floor_date(date, unit = "week")) %>% 
  group_by(candidate, week) %>% 
  summarize(number_of_stops = n())
```

    ## `summarise()` has grouped output by 'candidate'. You can override using the `.groups` argument.

``` r
ggplot(data = weekly_campaign_stops, mapping = aes(x = week, y = number_of_stops, color = candidate)) +
  ggtitle("Number of campaign stops leading up to the 2016 election")+
  geom_point()+
  scale_color_manual(breaks = c("Clinton", "Trump"),
                        values=c("#3182bd", "#de2d26"))
```

![](README_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

## Extent to which the names “Casey” and “Riley” were used for babies of both sex male and female.

Code and Visualization:

``` r
library(ggplot2)
library(dplyr)
library(babynames)

babynames_riley_casey <- babynames %>% 
  filter(name == "Riley"|name == "Casey")

ggplot(data = babynames_riley_casey, aes(x=year,y=prop, summary = sex, color=sex))+
  ggtitle('Comparison of Casey and Riley')+
  geom_line()+
  facet_wrap(~name)+ 
  labs(x = "Year", y = "Proportion")
```

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

\`\`\`
