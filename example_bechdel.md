---
title: "Example for Introduction to Linear Regression"
author: "Christina Knudson & Lisa Lendway"
output:
  html_document:
    theme: sandstone
    df_print: paged
    keep_md: true
---


```r
library(tidyverse) #used for visualization, summarization, and basic wrangling
library(ggridges) #used for making density ridge plots
library(broom) #used for "prettier" and easier to work with model output
library(fivethirtyeight) #datasets
```

# Bechdel Test

Before we jump into the statistics, take time to read this [fivethirtyeight](https://fivethirtyeight.com/features/the-dollar-and-cents-case-against-hollywoods-exclusion-of-women/) article. We are going to be using more or less the same data they used in that article. The cartoon by Alison Bechdel that test comes from is shown here:

![](bechdel_cartoon.jpg)

Throughout the analysis, you should use the *bechdel_1990up* dataset that removes missing values and only includes movies that were made in 1990 or later.


```r
bechdel_1990up <-
  bechdel %>% 
  filter(year>1989, 
         !is.na(budget_2013), 
         !is.na(intgross_2013)) 
```

# Exploratory Work

(@) The code below summarizes the percentage of films that pass for each of the 24 years that we have data. It also counts the number of films by year. Use this code and pipe into a *ggplot* to create a graph of *pass_pct* by year. Represent it as both a point and a line and size the points by *n*. (HINT: remember the *size* aesthetic). Describe the trend you observe. (Remove the `eval=FALSE` piece if you want this to run when you knit it)


```r
bechdel_1990up %>% 
  group_by(year) %>% 
  summarize(pass_pct = mean(binary=="PASS"),
            n = n())
```

(@) Create a graph that shows the distribution of *intgross_2013*, the film's international gross in 2013 inflation adjusted US dollars. Describe the distribution.



(@) Now compare the distribution of *intgross_2013* by *binary* (PASS if the film passed the test and FAIL if it did not). Describe the differences, if any.




(@) Also create a graph that compares the distribution of *budget_2013*, the film's budget in 2013 inflation adjusted US dollars, by *binary*. Describe the differences, if any.




(@) Create a plot that examines the relationship between *budget_2013* and *intgross_2013* (use *intgross_2013* as the response variable). Color the points by *binary*. Describe what you observe.



## Fitting and Interpreting Models

According to the *fivethirtyeight* article, there is a perception in Hollywood that "films featuring women do worse at the box office". We aim to investigate this using the *bechdel_1990up* data. We have already started this investigation in the previous section with some exploratory work. Now we will fit some models to help solidify our observations. 

(@) Fit a model that uses *budget_2013* to explain *intgross_2013*. Interpret both coefficients in the context of the data.

(@) Use the model to find the fitted value and the residual for the movie "Cloudy with a Chance of Meatballs".

(@) Test if *budget_2013* has a linear relationship with *intgross_2013*. 

(@) Fit a model that uses just the *binary* bechdel test results to explain *intgross_2013*. Interpret both coefficients in the context of the data.

(@) Use the model to find the fitted value and the residual for the movie "Cloudy with a Chance of Meatballs".

(@) What is the hypothesis test actually testing in the *binaryPASS* row of the model table? So, what do you conclude?

(@) Fit another model that uses both *budget_2013* AND *binary* to predict *intgross_2013*. 

(@) Interpret all three coefficients in the context of the data. How does the `binaryPASS` coefficient in this model compare to its coefficient in the model with only that variable? Explain why.

(@) Represent the previous model on a graph with *intgross_2013* on the y-axis and *budget_2013* on the x-axis.

(@) Use the **anova** method to test if *binary* is useful in the model that already includes *budget_2013*.

(@) Find the fitted value and the residual for the movie "Cloudy with a Chance of Meatballs". 

(@) Try building other models that use more variables. Can you find any more useful variables?


