---
title: "LPM Model fit problem"
subtitle: ""
author: "Themenfeld SS 2021"
date: "2021-05-25"
output:
  html_document:
    keep_md: yes
  pdf_document: default
---



There has been much interest in the question whether the presence of 401(k) pension plans, available to many U.S. workers, increases net savings.  
The data set `k401ksubs` contains information on net financial assets (`nettfa`), family income (`inc`), a binary variable for eligibility in a 401(k) plan (`e401k`), and several other variables. In the following, you are asked to run a linear regression that predicts eligibility.




```r
glimpse(k401ksubs)
```

```
## Rows: 9,275
## Columns: 11
## $ e401k  <int> 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, …
## $ inc    <dbl> 13.170, 61.230, 12.858, 98.880, 22.614, 15.000, 37.155, 31.896,…
## $ marr   <int> 0, 0, 1, 1, 0, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1, …
## $ male   <int> 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, …
## $ age    <int> 40, 35, 44, 44, 53, 60, 49, 38, 52, 45, 61, 40, 48, 60, 43, 43,…
## $ fsize  <int> 1, 1, 2, 2, 1, 3, 5, 5, 2, 1, 3, 6, 3, 2, 5, 1, 2, 2, 2, 2, 5, …
## $ nettfa <dbl> 4.575, 154.000, 0.000, 21.800, 18.450, 0.000, 3.483, -2.100, 5.…
## $ p401k  <int> 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 1, …
## $ pira   <int> 1, 0, 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, …
## $ incsq  <dbl> 173.4489, 3749.1128, 165.3282, 9777.2539, 511.3930, 225.0000, 1…
## $ agesq  <int> 1600, 1225, 1936, 1936, 2809, 3600, 2401, 1444, 2704, 2025, 372…
```

## 1 Tasks

### 1.1 Fitting and interpreting

* How many families are eligible and how many are not eligible for participation in a 401(k) plan? Present the absolute numbers and the respective fractions.  



> For a total of  **9275** observations, **3637** families are eligible for participation in a 401(k) plan, while **5638** are not eligible.

* Estimate a linear probability model explaining 401(k) eligibility in terms of income, age, and gender. Include income and age in quadratic form, and report the results in the usual form.  



> $\begin{align*}
e401k & = -0.5063 + 0.0124 income + 10^{-4} income^{2} + 0.0265 age + (-3\times 10^{-4}) age^{2} + (-0.0035) male + u \\  
R^{2} & = 9.43\% ;    Sample size = 9275 \\
\end{align*}$  

* Interpret the coefficients.  

> While negative propabilities (coefficients with negative foresign) do not make sense in general, the negative coefficient for $male$ can be interpreted in a way, that it only increases the propability if the respondent is female ($1-male$).  
The coefficient for income seems to have the biggest influence given the reletively big factor $income$ and the value for the coefficient.  
The coefficients for $age$ - especialy with it's relatively small factor $age$ - and $income^{2}$ have rather small values and do not seem to have much of an impact on the total propability.

* Obtain the fitted values from the linear probability model estimated in part (ii). Are any fitted values negative or greater than one?



> The smallest fitted value from the model is 0.0299172 (positive), while the largest fitted value is 0.6971899 (smaller than one).

### 1.2 Discussing model fit

* Using the fitted values $\hat{e401k}_{i}$ from part (iv), define $\tilde{e401k}_{i} = 1$ if $\tilde{e401k}_{i} \ge 0.5$ and $\tilde{e401k}_{i} = 0$ if $\tilde{e401k}_{i} < 0.5$. Out of 9,275 families, how many are predicted to be eligible for a 401(k) plan?  



> Out of  **9275** families, **2460** families are predicted to be eligible for a 401(k) plan, while **6815** are not.

* Use the variable $\tilde{e401k}_{i}$ to compute the overall percent of correctly predicted/classified observations (families).  

> The overall percent of correctly predicted/classified observations (families), using $\tilde{e401k}_{i}$ is 47.44%.

* Now compute the percent correctly predicted/classified for both eligible and non-eligible families. What
does this suggest regarding your previously computed measure of model fit?

### 1.3 Writing a function

Now write a function that accepts a vector thresholds for predicting a family as eligible vs non-eligible. For
example, the function accepts c(0.5, 0.6) as an input parameter.
The function takes the data and the formula as an input. The function performs the following steps:
• It runs the regression (specified in the formula-argument)
• Then, it uses the threshold and computes the overall percent of correctly classified observations and
also the the percent correctly predicted/classified for both eligible and non-eligible families.
