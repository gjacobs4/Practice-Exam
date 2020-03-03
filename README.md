---
title: "Practice Exam"
author: "Genevieve Jacobs"
date: "2/27/2020"
output: md_document
---

# Practice Exam

# This is my in-class attempt at the practice exam from February 27th. I am uploading the unfinished attempt to github.

This practice exam asks you to do several code wrangling tasks that we have done in class so far. 

Clone this repo into Rstudio and fill in the necessary code.  Then, commit and push to github.  Finally, turn in a link to canvas. 



```{r echo = F}
rm(list =ls())

library(tidyverse)
library(ggplot2)
library(nycflights13)

# flights
# weather
```


Make a plot with three facets, one for each airport in the weather data.  The x-axis should be the day of the year (1:365) and the y-axis should be the mean temperature recorded on that day, at that airport.

```{r}
library(lubridate)
weather
data1 = weather %>% mutate(day_of_year = yday(time_hour)) %>% group_by(day_of_year, origin) %>% mutate(avgtemp = mean(temp))

ggplot(data1, aes(x=day_of_year, y=avgtemp, color=origin)) + geom_point() + facet_wrap(~origin, nrow = 3)
```


Make a non-tidy matrix of that data where each row is an airport and each column is a day of the year. Each element is the average temp from the plots above.

```{r}

data2 = weather %>% mutate(day_of_year = yday(time_hour)) %>% group_by(day_of_year) %>% mutate(avgtemp = mean(temp)) %>% pivot_wider(names_from = origin, values_from = avgtemp)

data2

data1point5 = weather %>% mutate(day_of_year = yday(time_hour)) %>% group_by(day_of_year) %>% summarise(mean(temp, na.rm = TRUE))



```


For each (airport, day) contruct a tidy data set of the airport's "performance" as the proportion of flights that departed less than an hour late. 
```{r}
```

Construct a tidy data set to that give weather summaries for each (airport, day).  Use the total precipitation, minimum visibility, maximum wind_gust, and average wind_speed.  
```{r}
```

Construct a linear model to predict the performance of each (airport,day) using the weather summaries and a "fixed effect"(dummy/categorical variable for airport) for each airport.  Display the summaries.  
```{r}

lm(performance~origin +..., data)

```

Repeat the above, but only for EWR.  Obviously, exclude the fixed effect for each airport.
```{r}
```