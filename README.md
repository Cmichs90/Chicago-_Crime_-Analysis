# Chicago-_Crime_-Analysis

![](Crime_Image.jpg)

## Project Background
I love Chicago and would want to live in that city someday but with the high rise in crime rate this might in the long run affect its economic significance. Amidst the inflation in the country, residents want to feel safe in their environment but with the increasing crime activities that might be questioned as there is no promising measure to tackle this situation. The primary objective is to not only identify potential threats but also to discern patterns, foresee future increases with the aim of providing actionable insights that can inform strategic interventions and policies to enhance public safety, address vulnerabilities, and foster a resilient and secure urban environment for all residents and visitors.

** All Dataset use in this project are real and provided by leveraging the City of Chicago's Data Portal, crime data spanning from 2021 to 2023 [here](https://data.cityofchicago.org/browse?q=crime+dataset+2021&sortBy=relevance&pageSize=20&limitTo=datasets)

## Introduction

This is a R project on crime rate in chicago. This project is to inform and understand of there are any variable affecting crime rate in chicago and how the government can work together in mitigating risks and provide a better community and environment. 

** This was my Master's Degree Presentation

##  Problem Statement

1.	How does the age demographic contribute to crime patterns?
2.	What temporal patterns exist?
3.	Which locations consistently have the highest crime rates, and what factors contribute to their designation as hotspots?
4.	Does law enforcement presence affect crime occurrence?

## Skills/Concept Demonstrated

This analysis is a linear regression in R Studio to identify if any relationship exists. 
-  Dependent variable considered at various points is Arrest, as the frequency of reported crime in Chicago.  
-  Independent variables include demographic factor, time of the day and day of the year and other factors.
-  Visualisation
-  Predictive Analysis
  

## Analysis

###   Q1:  How does the age demographic contribute to crime patterns

Showing Age Distribution Visualisation           |             Analysis 

:----------------------------------------------: | :-----------------------------:

![](Distribution_of_Age.png)                     |  ![](R_Analysis.png)         


### Analysis Summary

The coefficient of victimization primary homicide is 245.14 with a p-value of 0.00162. This indicates that, on average, individuals involved in homicides tend to be older compared to other victimization types, and this difference is statistically significant. The coefficient of victimization primary non-fatal is -215.80 with a p-value of 0.27567. This suggests that there is no statistically significant difference in age between non-fatal victims and other victimization types. The coefficient of victimization primary robbery is -1632.19 with a p-value of 0.05679. While the p-value is close to 0.05, indicating some evidence of a difference, the coefficient suggests that individuals involved in robberies tend to be younger, although this relationship is not statistically significant at the conventional level of significance (p < 0.05). The coefficient of incident primary homicide. is 20.16 with a p-value of 0.78167. This indicates that there is no statistically significant difference in age between incidents involving homicide and other incident types. The coefficient of incident primary non-fatal is -746.56 with a p-value of 0.39443. Like non-fatal victimization, there is no statistically significant difference in age between non-fatal incidents and other incident types. The coefficient of incident primary robbery is 2059.66 with a p-value of 0.01673. This suggests that, on average, individuals involved in robberies tend to be younger compared to other incident types, and this difference is statistically significant.


## Q2:  What temporal pattern exist

Number of Crime over the years                          |             Temporal Pattern of Incident types over the years 

:----------------------------------- -----------------: | :------------------------------------------------------------------:

![](Number_of_Crime_over_the_years.png)                           |  ![](Showing_period_of_the_Crime.png)   

The result shows that there is a pattern with an increase from day 100 to day 210. which falls between June to Early September with battery been at its highest peak. 


Showing Relationship                                    |             Analysis Result 

:----------------------------------- -----------------: | :------------------------------------------------------------------:

![](Showing_Relationship.png)                           |  ![](Linear_Regression_Analysis.png)   


###  Analysis Summary

The linear regression model indicates that there is no significant linear relationship between the month and the count of incidents. The R-squared value of 0.1082 suggests that the model explains only a small portion of the variance in the count of incidents.



## Q3:  Which locations consistently have the highest crime rates, and what factors contribute to their designation as hotspots.

How crime is distributed                                |  Show the most affected Zip Code that has been mostly imparted by crime   |  Top 20 Location group by count  

:----------------------------------- -----------------: | :------------------------------------------------------------------:  | :-----------------------------------:

![](Showing_How_crime_are_distributed.png)                 |  ![](Zip_Code_Affected.png)                               | : ![](TOp20_Location_count_by_group.png)   


###  Analysis Summary


Image 1: This result shows that crime is uniformly distributed across chicago describing assault, homicide, robbery and others. 

Image 2 : The result from this bar chart shows that crime is largely carried out in some location that other Zip codes like 60600 - 60650 has the highest number of crime occurrence. with more occurrency between 60600-60640 where counts reach nearly 600 unique incidents.  The visualization was done using the library called ggplot in R.   This was arrived by using the variables case count and category.


## Q4: Does law enforcement presence affect crime occurrence?


Crime type and Arrest Number                             

:----------------------------------- -----------------: 

![](crime_and_Arrest_Number.png)     

## Summary 

Looking at the bar chart, its show that battery has the highest crime in chicago with a high number more than 5000 and a total number of less than 500 Arrest made could this be that at each district of the police ward there are no enough police to enforce law. 


# Other Analysis: 

Prediction: Predicting the number of crimes per day


# Function to calculate day number of the year
day_of_year <- function(month, day) {
  cum_days <- cumsum(c(0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30)[1:month])
  cum_days[month] + day
}

# Calculate day number of the year for each row
filtered_df$DayOfYear <- mapply(day_of_year, filtered_df$MONTH, filtered_df$DAY_OF_WEEK)

# Print first 10 rows of two columns

# This may show a little bit off  but correct most of the times

print(head(filtered_df[, c("DATE","DayOfYear", "Primary.Type.x")], 10))
##              DATE DayOfYear Primary.Type.x
## 1   1/1/1996 4:40         2           <NA>
## 2   1/1/1996 4:40         2           <NA>
## 3  6/17/2012 0:38       152           <NA>
## 4   1/1/1996 0:15         2           <NA>
## 5  3/8/2022 15:27        62           <NA>
## 6   1/3/1996 1:00         4           <NA>
## 7  1/3/1996 19:02         4           <NA>
## 8  7/26/2015 2:34       182           <NA>
## 9  1/5/2016 15:36         3           <NA>
## 10 7/22/2018 5:34       182           <NA>

#Counting the number of crimes and grouping them by day of the year. 
grouped_DayOfYear <- filtered_df %>%
  group_by(DayOfYear) %>%
  summarise(Count = n_distinct(CASE_NUMBER))

# Rename the "old_column" to "new_column"
colnames(grouped_DayOfYear)[colnames(grouped_DayOfYear) == "Count"] <- "Number_of_Crimes"

grouped_DayOfYear
## # A tibble: 84 × 2
##    DayOfYear Number_of_Crimes
##        <dbl>            <int>
##  1         1              538
##  2         2              454
##  3         3              401
##  4         4              395
##  5         5              390
##  6         6              469
##  7         7              612
##  8        32              470
##  9        33              318
## 10        34              329
## # … with 74 more rows
# Create a line chart
ggplot(grouped_DayOfYear, aes(x = DayOfYear, y = Number_of_Crimes)) +
  geom_line() +
  labs(title = "Number of crimes over the year",
       x = "Day of Year",
       y = "Number of crimes over the year") +
  theme_minimal()

# Developing A simple regression model

### Split the data into training and testing sets
split <- sample.split(grouped_DayOfYear$Number_of_Crimes, SplitRatio = 0.75)
Training <- subset(grouped_DayOfYear, split == TRUE)
Testing <- subset(grouped_DayOfYear, split == FALSE)
# Fitting the regression model and showing the summary
Reg_model <- lm(Number_of_Crimes ~ DayOfYear, data = Training)
 
summary(Reg_model)
## 
## Call:
## lm(formula = Number_of_Crimes ~ DayOfYear, data = Training)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -233.57 -110.36   -8.01   82.42  424.74 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 521.4958    36.0168   14.48   <2e-16 ***
## DayOfYear     0.4074     0.1835    2.22   0.0302 *  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 152.9 on 61 degrees of freedom
## Multiple R-squared:  0.07474,    Adjusted R-squared:  0.05957 
## F-statistic: 4.927 on 1 and 61 DF,  p-value: 0.03016
# Making prediction on the testing data set
predictions <- predict(Reg_model, newdata = Testing)

# Creating a data frame
Result <- data.frame(Test = Testing$Number_of_Crimes , Prediction = predictions)
Result$Difference <- Result$Test - Result$Prediction
 
head(Result, n=25)
##    Test Prediction  Difference
## 1   395   523.1253 -128.125296
## 2   318   534.9389 -216.938939
## 3   291   536.1610 -245.161040
## 4   452   536.9758  -84.975774
## 5   453   546.3452  -93.345214
## 6   516   558.9736  -42.973590
## 7   817   573.2314  243.768565
## 8   645   585.0451   59.954923
## 9   923   585.8598  337.140189
## 10 1025   595.6366  429.363382
## 11  638   609.8945   28.105538
## 12  960   610.7092  349.290804
## 13  868   620.8934  247.106629
## 14  557   622.1155  -65.115472
## 15  631   622.9302    8.069794
## 16  565   633.5217  -68.521747
## 17  484   634.3365 -150.336481
## 18  616   645.7428  -29.742756
## 19  453   646.9649 -193.964857
## 20  641   648.1870   -7.186958
## 21  445   658.3711 -213.371133
Model evaluation
#Mean Squared Error (MSE), R-squared, etc.
mse <- mean((predictions - Testing$Number_of_Crimes)^2)
r_squared <- 1 - (sum((Testing$Number_of_Crimes - predictions)^2) / sum((Testing$Number_of_Crimes - mean(Testing$Number_of_Crimes))^2))

cat("Mean Squared Error:", mse, "\n")
## Mean Squared Error: 38187.65
cat("R-squared:", r_squared, "\n")
## R-squared: 0.07736505
# Fit an AR model
grouped_DayOfYear$Number_of_Crimes <- as.numeric(grouped_DayOfYear$Number_of_Crimes) #set as numeric

#fitting AR model
#ar_model <- arima(grouped_DayOfYear$NumberofCrashes, order = c(p = 1, d = 0, q = 0))
# Fit an AR model
ar_model <- ar(grouped_DayOfYear$Number_of_Crimes, order.max = 1)
# Print the model summary
print(summary(ar_model))
##              Length Class  Mode     
## order         1     -none- numeric  
## ar            1     -none- numeric  
## var.pred      1     -none- numeric  
## x.mean        1     -none- numeric  
## aic           2     -none- numeric  
## n.used        1     -none- numeric  
## n.obs         1     -none- numeric  
## order.max     1     -none- numeric  
## partialacf    1     -none- numeric  
## resid        84     -none- numeric  
## method        1     -none- character
## series        1     -none- character
## frequency     1     -none- numeric  
## call          3     -none- call     
## asy.var.coef  1     -none- numeric
# Print the model coefficients
print(ar_model$order)
## [1] 1
print(ar_model$ar)
## [1] 0.7362339
# Predicting the next 'n' steps
n_steps <- 10
predictions <- predict(ar_model, n.ahead = n_steps)

# Print 10 forecast values
print(predictions$pred)
## Time Series:
## Start = 85 
## End = 94 
## Frequency = 1 
##  [1] 618.7399 611.9223 606.9030 603.2076 600.4869 598.4839 597.0091 595.9234
##  [9] 595.1241 594.5355
#save a copy of the data set
write.csv(filtered_df , file = "comfort_Chicago_CrimeData2.csv", row.names = FALSE)


## Predictive Analysis Summary: 
Crimes might slowly decrease over time in the prediction. But predictions aren't 100% perfect— i need more data to make better reasoning.


#  Recommendation and conclusion: 

1.	 Increase law enforcement presence in identified hotspots.
     Place like Austin community with the highest crime rate of 4172 and Zip code 60624 should be on red alert and also have stringent law enforcement implementation. 
2.	 Implement targeted interventions during peak crime periods.
3.   Tailor crime prevention strategies for ages 20-29.
4.   use socio-economic and demographic insight for community development and crime reduction. 

Providing actionable insights for law enforcement, policymakers, and community leaders, this research aims to enhance public safety in Chicago. Implementing recommended strategies can significantly reduce crime rates, positively impacting residents, tourists, and the community.


![](thank_you.jpg)    


















