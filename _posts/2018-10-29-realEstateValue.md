---
title: Real estate value analysis
hidden: false
categories: EN data-analysis
tags: R data-analysis open-data
author: neonira
comments: true
permalink: re1
---

French government provides from time to time some data sets that are worth the analysis. A friend, gave me this [real estate data set](https://www.data.gouv.fr/fr/datasets/valeurs-immobilieres-economiques-et-financieres-de-1800-a-2015/#_), for analysis. 


### Data overview 

After the download of this file, that weights less than 200kb, many things appear at first glance. 

From a content point of view, data are provided for 3 countries, France, England and USA. They are organized as data series on a timeframe starting in 1800, up to 2015. 

From a data quality point of view, a good job have been accomplished. I mean, there are missing data when no statistics were available, and provided data come under a well organized serie, without any hole.  

From a style point of view, this appears to be a good Excel nightmare. As mentioned, we have data for 3 countries, but not the same data. For France, we got 27 series, 11 for England, and 12 for USA. But weirdness does not stop at those easy to notice issues. Some more subtles are lurking. First, some series have the same topics addressed by different authorities <cite class='comment'>e.g. England home prices</cite> or scope <cite class='comment'>e.g. France vs Paris home prices</cite>. Second, each data series is provided under the country currency, thus requiring a conversion to a pivot currency. That tasks is indeed eased as the conversion rate from the currency to euro based on year 2000, is provided for <cite class='kw'>GBP</cite> and for <cite class='kw'>USD</cite>. And third, data is presented in a well-formed and human readable format, but clearly not matching data analysis requirements. So, some data wrangling is required. 

### Data preparation

First I saved the file under a <cite class='kw'>.xlsx</cite> format instead of the provided <cite class='kw'>.xls</cite> format. 

Second, I added some columns to ease data handling

<table>
   <thead>
      <tr>name of the added column </th><th >Goal</th></tr>
   </thead>
<tbody>
      <tr><td>country</td><td>distinguish easily the country, source of the data</td></tr>
      <tr><td>category</td><td>categorize each data serie, in order to compare what is comparable</td></tr>
      <tr><td>unit</td><td>allows to manage conversion to a pivot currency</td></tr>
      <tr><td>coefficient</td><td>the multiplier of the units, to ensure comparisons using sames dimensions</td></tr>
      <tr><td>serie number</td><td>to allow serie selection when more than one is provided per country</td></tr>
</tbody>
</table>


I simply used <cite class='kw'>R package XLConnect</cite> to turn excel sheet into a  <cite class='kw'>R data.table</cite>.

### Data conversions

Following conversions were applied to the data

* countries are turned to a factor
* currencies are turned to EURO using respective conversion rate over the years, as provided by the data

### Data wrangling 

I used <cite class='kw'>R package tidyr</cite> to manage data wrangling. Mainly, I turned data series from 1800 to 2015, given in columns into two column, named <cite class='kw'>year</cite> and <cite class='kw'>value</cite>, keeping all the other columns, except the one named 'Séries' as I want English language output to be produced, and not French. 

Here is the main part of the code <cite class='kw'>sc is simple the index of the starting column name </cite>.

```r
dtx <- as.data.table(tidyr::gather(dtc, 'year', 'value', sc:ncol(dtc)))
dtx[, `:=`(year = as.integer(substring(year, 2)))]
```


### Diagramming

I relied on <cite class='kw'>R package ggplot2</cite> to do the job. Just need here to set up a diagram model, to be reused. 
I juste enforced the following

1. caption is desired to be at the top, using same color scheme for all diagrams, to ease reading
1. diagram title will be taken from the English label of the French serie
1. diagram abscisses are the years, generally full scaled from 1800 to 2015, sometimes restricted when it makes sense
1. diagram ordinates are values
1. theme is kept very simple and near the default provided natively by <cite class='kw'>ggplot2</cite>.

Here is the main part of the code <cite class='kw'>da is the data.table variable name </cite>.

```r
mc <- c('en' = 'red', fr = 'blue', us = 'green')
ggplot(da, aes(x = year, y = value, color = country)) + 
    geom_line() + 
    scale_color_manual(values = mc[as.character(unique(da$country))]) +
    ggtitle(da$Serie[1]) + 
    theme(legend.position = 'top')
```

### And the diagrams produced 

#### Home price index

![home price index](/images/realestate/ipl.png)

![home price index zoomed](/images/realestate/ipl_z.png)

![disposable income](/images/realestate/rdm.png)

![disposable income zoomed](/images/realestate/rdm_z.png)

#### Interest rates

![short time interest rate](/images/realestate/tict.png)

![long time interest rate](/images/realestate/tilt.png)

#### Economical context 

![Gross domestic product](/images/realestate/pib.png)

![Population](/images/realestate/tilt.png)

![Consummer price index](/images/realestate/ipc.png)

![Value of investment in stocks](/images/realestate/via.png)

### Conclusion  

Business analysis can now be executed. Let's wait for my friend to provide its results. 
Will share them in a second blog post. 

