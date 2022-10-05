# OLS Linear Regression


## Overview

This module allows you to OLS linear regression estimation with the addition that you can control for fixed effects according to some choice variables. Moreover, you can use robust methods (heteroskedasticity and clustered std. errors) to estimate the variance covariance matrix. 

##  Inputs
The OLS linear regression model can be called by using the class *ols* in the main file. To call this class, you need the following inputs:

- *data* is the dataframe where you stored your data you want to pass in the ols model.
- *x* is the list of strings of all explanatory variables you want to use to explain y. I mean the strings of the columns that store your x's variables.
**It is very important that you pass a list of strings even if your explanatory variable is just one variable.**
- *y* is the string of the column that stores your dependent variable in your dataframe.
- *cons* is True by default, but if you want to regress without intercept, just declare *cons = False* .
- *fixed_eff* by default is an empty list. However, you can pass a list with the string of all variables you want to use for fixed effects. For example, if you have a panel dataset of countries years, you can pass a list of string of the variable that stores countries and a string for the variable that stores years.
- *method* is "non_robust" by default, but if you want to a Heteroskedastcity robust variance covariance matrix, just declare *method = 'robust'*  Moreover, if you want to estimate the variance covariance matrix with clustered method, you have to pass *method = 'cluster'*.
- *cluster* by default is False. However, if you decided to use a clusterd estimation, you have to pass the string for the variable you want to use as clusters.

## Features
- To summarize the results, just call "your object name" . *summary()*. For now, it will print just the table with betas, std, t, p value, and confidence
interval.

- Use *int_vars().get('beta')* if you want to obtain beta coefficients.
- Use *int_vars().get('std')* if you want to obtain standard deviation for betas.
- Use *fitted()* if you want fitted values.
- Use *residuals()* if you want residuals.
- Use *summary()* if you want a table form summary of the estimation.

## Example 

To initialize the model (suppose the module is imported *as reg*:

```
model  = reg.ols(data = df, x=['exper','expersq','kidslt6','kidsge6'],y = 'lwage')
```

To call the informative summary:
```
model.summary()
```

And here is the output:
```
Linear regression
---------------------------------------------------------------
lwage      coefficient           se          t    p_value       low 95       high 95
-------  -------------  -----------  ---------  ---------  -----------  ------------
exper       0.0456439   0.0141809     3.21869        0      0.0178494    0.0734385
expersq    -0.00101304  0.000417998  -2.42356        0.02  -0.00183232  -0.000193768
kidslt6     0.0314494   0.0892375     0.352424       0.72  -0.143456     0.206355
kidsge6    -0.0345768   0.0283234    -1.22079        0.22  -0.0900906    0.020937
cons        0.875164    0.120301      7.27478        0      0.639374     1.11095
---------------------------------------------------------------

