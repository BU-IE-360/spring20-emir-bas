---
title: "IE 360 Project Report Group 9"
author: "Ali Oğuz Bilgiç - Musab Emir Baş - Selman Berk Özkurt - Yusuf Hançer"
date: "04 07 2020"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Introduction

This project is about forecasting the number of sales of the next day. Trendyol provided past data for that project. Historical recordings of 8 different products were given with their id, date of the event, price, number of products sold, number of visits to the page of the product, number of times that products were put into the basket of the customer, number of times that product was signed as favourite, sales numbers of the category, sales numbers of the category for that brand, visit numbers of the category and visit number of Trendyol. After that, it is required to estimate sales number of the next day for those products. Product definitions are shared in Table 1.

![Table 1. Product Definitions](images/Table1.png)

In the project definition, importance of other details such as day of the week or special occasions was specified. With this object, site level data was equipped. Black Friday or similar events are determinable after that. It was announced that in the process of estimating, extraneous goods are also useable. 
Prepared application programming interface lets this project to be performed as a competition. Everyday submissions are required after having, manipulating and developing  forecast models. Apparently, model is applicable in case of arranging sufficient inventory or service degrees. 


## Related Literature

Before preparing this project, it was required to study on DataCamp courses to understand the essence of the R for time series. There, besides all other courses, “Manipulating Time Series Data With xts and zoo in R”, “Time Series Analysis in R”, “Forecasting in R”, and “Forecasting Product Demand in R” courses were studied for that specific project.
Terms like xts, White Noise (WN), Random Walk (RW), Trends, seasonality, and cyclicity, or Mean Absolute Error (MAE),  Mean Absolute Percentage Error (MAPE) were studied on to shape the project model better with Autoregression (AR), Simple Moving Average (MA) and ARIMA(AutoRegressive Models Integrated Moving Average).**(Kullanılmayanları çıkaralım mı)** Those applications will be used and explained in the following parts.


## Approach

At the project, beginning code was provided. It ensured the code submissions to the application programming interface for each product separately with group number on it. Then the code for the estimation of the number of sales for the next day begins. In the process of coding, necessary libraries like xts, gtrendsR or data.table were added.
At the beginning of the study, number of products were checked. Those 8 products were needed to be split up to work on each item distinctively. Thus, a list named ‘xdata’ was created to save each product separately day by day with the help of a for loop. In that loop, for every product, an xts object is created and added to the ‘xdata’. Anymore, there is an xts object for each product that was provided within the past data.
Provided past data has some blank days in it. To prevent this situation to create greater problems, all blank days was fulfilled. **To do so, ….?** . After that, there is not any blanks in the data. Sales estimates might be worked on.
For estimating sales sold_count is a strong element. As first and basic estimation tool, linear model of sold_count was preferred. Linear component of each item was added with the data of the last 21 days by examining sold_count data as a time series. Then, for every product, a trend component was added as an attribute to be used as a regressor thereafter. For that calculation, lasttrend function was preferred. Then, to fulfill ‘-1’ parts spline interpolation was used because it provides more unbiased and smoother estimates.
For another tool Google Trends data was preferred. Searches made on Google by buyers could be classified, modified and used for estimation. Google Trends data might be had yearly by weeks, or from last month by days. Monthly data was binded into yearly data to be used as a whole. 
Estimating today’s sales numbers from the data of the two days before was another idea. xdata_lag list was created for that purpose. To be used before predicting regressors, from the data of two days before, sold_count data of the today was tried to predict. Output of the part until this point and output of the continuing part were compared and according to observations more dependable one submitted.
Another approach was the importance of the last 3 weeks’ weekly data for each day. So this approach was for the last 22 days. sold_count data of 7 days before, 14 days before and 21 days before were added for each product everyday. This step was applied both to xdata and xdata_lag. If effectiveness of that approach is not satisfying, in the loop which was written to create a linear model, it was not going to be used.
Approaches that are improved till here were for creating a linear model. After using all **(?)**, intercept was removed. Here, a while loop checks p values of results of approaches. Until every regressor has a p value less than 0.05 while loop works. One by one, linearly they**(?)** are removed by beginning with the highest p valued. Finally, last model developed is returned. Models were formed for both xdata and xdata_lag. Estimations were done with lapply function. After predicting, results were submitted. 
From observations, products provided better results for different approaches. In this case, for product 1,2,3 and 5, data of 2 days before gave more dependable results. However, for the rest, predicting with lags were more dependable. Submission were made accordingly. 


## Results & Conclusion

After all, it is clear that predicting future sales is a difficult task for daily life. In times of crisis it is even harder. For that work, in that term, some daily results were really close to real number of sales though some days it was further. Covid 19 crisis, as expected, changed norms of the shopping and some days, number of sales waved in that one month as different from estimates according to last data. So, outliers are the real challenger here and predicting those days is a necessity by means of holding inventory and being prepared days before.


## Code

```{r}

```
