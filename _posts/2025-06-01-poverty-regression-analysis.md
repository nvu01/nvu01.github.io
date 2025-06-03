---
layout: post
title: Socioeconomic Factors Impacting Poverty in U.S. Counties
description: >
  A regression-based analysis of how socioeconomic variables drive poverty rates across 854 U.S. counties, using data from the U.S. Census Bureau.
image: /assets/img/posts/kostiantyn-li-1sCXwVoqKAw-unsplash.jpg
subtitle: "A Data-Driven Approach to Understanding Poverty Using Multiple Linear Regression"
date: 2025-06-03
tags: [regression, public policy, socioeconomic data, poverty, census data]
---

This post summarizes my capstone project for my program in Data Analytics at WGU. I used **multiple linear regression** to investigate how socioeconomic factors influence poverty rates across U.S. counties.

[<i class="icon-github"></i> GitHub Repo](https://github.com/nvu01/BSDA-Capstone-Project)

* toc
{:toc .large-only}

## Project Overview

Poverty is a multifaceted issue that is influenced by many factors such as income levels, education, employment rates, healthcare access, public programs and housing conditions. These variables interact in ways that are not immediately apparent, and their combined effects on poverty rates can vary widely across different regions. Data analysis provides objective insights rather than relying on surface-level observations. As a data analyst, I wanted to answer a critical question: **What are the most important socioeconomic factors that explain poverty rates in U.S. counties, and how reliably can we model those rates using multiple linear regression?**

In this project, I applied a rigorous, statistics approach to analyze data from the U.S. Census Bureau’s 2023 American Community Survey. The goal was not just to model poverty, but to surface meaningful insights that could guide policy and resource allocation.

I used Jupyter Notebook as the primary development platform. The whole analytical process wwa done using Python libraries such as pandas for data manipulation, Matplotlib and Seaborn for visualization, NumPy for numerical operations, statsmodels for regression and statistical testing, and scikit-learn for scaling and model validation.

## Description of Dataset

The dataset for this project comes from the U.S. Census Bureau’s 2023 American Community Survey (ACS) 1-Year Estimates, a trusted national source of socioeconomic data. Publicly available on data.census.gov, the dataset includes relevant indicators like income, education, unemployment, and public assistance, making it well-suited for analyzing poverty predictors at the county level.

A key limitation is that the poverty rate is based on the Official Poverty Measure (OPM), which doesn’t factor in regional living costs or non-cash benefits like SNAP or housing subsidies. This could limit how socioeconomic factors are interpreted. According to the Census Bureau’s 2023 report, the OPM showed a national poverty rate of 11.5%, while the more comprehensive Supplemental Poverty Measure (SPM) reported 12.7%, underscoring the impact of additional costs and public assistance income on poverty assessments.

## Data Collection

The data were collected using API requests to the U.S. Census Bureau’s 2023 ACS 1-Year datasets. The data collection process required learning how ACS data is structured. I studied Census Bureau documentation to understand table formats, variable naming, and geographic codes like the ucgid, which was essential for accurate county-level API requests. 

Initially, I planned to manually search for variable and geographic codes, but I later developed a more efficient method. I created a Python script that searches downloaded metadata files for variable codes based on table IDs and label keywords. This tool handles case and spacing issues, reducing human error. Part of the code was adapted from a Stack Overflow thread, which I cited.
```
Code for variable code retrieval
```

## Data Wrangling

Data from ACS tables were saved as .json files, parsed using Python, and combined into a single county-level dataset with Pandas. During data preparation, I renamed coded headers to descriptive variable names, converted data types, and addressed missing or special values by imputing based on 2022 ACS data. I also removed redundant columns and combined related variables to enhance usability. The cleaned dataset was then saved as a .csv file for modeling.

## Summary of Data Analysis Methods

I began EDA with descriptive statistics to examine central tendencies and spread. This is followed by calculating a correlation matrix and VIF to detect multicolinearity. I dropped or transformed any predictor whose VIF topped 5. To explore relationships between the response and explanatory variables, I used pairplots and scatter plots. To address nonlinearity and skewness in the data, I applied appropriate transformations based on the distribution and each variable's relationship with the response: log transformation for heavy right-tails, log1p when zeros appeared, and square-root for moderate skew.

The main analytical approach was a multiple linear regression method, which allowed me to quantify relationships between socioeconomic factors and poverty rates while considering the influence of multiple variables simultaneously. Specifically, the project used ordinary least squares (OLS) model which allowed a straightforward interpretation of coefficients, significance testing and model evaluation.

To evaluate the model’s predictive performance, I used metrics such as R-squared on both the training and test sets, adjusted R-squared, and mean squared error (MSE) on the test set. These metrics provided insight into how well the model fit the training data and how accurately it predicted poverty rates on new, unseen data.

To evaluate the role of socioeconomic factors in explaining poverty rates across U.S. counties, both a global and individual hypothesis testing framework will be used.
- Global hypothesis (F-test): This test evaluates whether the full set of predictors contributes to explaining poverty rates.
  - Null hypothesis: All regression coefficients are equal to zero 

    $$
    H_0:\;\beta_1=\beta_2=\dots=\beta_k=0
    $$

  - Alternative hypothesis: At least one regression coefficient is not equal to zero  

    $$
    H_1:\;\text{at least one } \beta_i \ne 0
    $$

- Individual hypotheses (t-test for each coefficient): These tests assess the significance of each predictor.
	- Null Hypothesis: The coefficient for predictor i is zero.  

    $$
    H_0:\;\beta_i = 0
    $$

	- Alternative Hypothesis: The coefficient for predictor i is not zero.  

    $$
    H_0:\;\beta_i \neq 0
    $$

To evaluate the relative importance of each socioeconomic factor in explaining poverty rates, I also used the standardized coefficients from the multiple linear regression model. These coefficients were obtained by scaling all independent variables using MinMaxScaler before fitting the model. This will ensure that the predictors are on the same scale.

For the baseline model and the improved model, I implemented residual analysis to verify model assumptions and ensure the model’s validity. OLS regression relies on several assumptions: linearity of relationships between predictors and the dependent variable, homoscedasticity (constant variance of residuals), independence of residuals, and normally distributed errors. The analysis included visualizations such as residual plots, histogram and boxplot of residuals, and Q-Q plot. This diagnostic step helped confirm whether the use of OLS and the resulting hypothesis tests were valid.

Finally, to address issues identified in model diagnostics, I applied several refinement methods. The response variable was transformed to reduce heteroscedasticity and improve linearity. An interaction term was added to improve model accuracy when the effect of one variable depends on another. Robust standard errors (HC3) were used to produce more reliable p-values in the presence of heteroscedasticity.

## Project Outcomes

- **Predictive Power**: My refined regression model worked well and explained 79.6% of the variance in training data and 83.1% in the test set. That’s high, especially for social data, where perfect predictions are rare. 

- **Overall Model Significance:** Based on the F-test result, the final model was statistically significant overall (p < 0.001).

- **Model Validity:** 
  - Residual vs fitted plot: Residuals are randomly scattered around zero with consistent spread across fitted values. This means there is no major heteroscedasticity. A few mild outliers are present.

![Residual vs fitted plot]()   

  - Residuals vs predictors: No strong patterns or funnel shapes. This supports the assumption of constant variance and linearity across predictors.

![Residuals vs predictors]()

  - Histogram & boxplot of residuals: Distribution is roughly normal, bell-shaped, and symmetrical. The median is near zero, with a few mild upper-end outliers.

![Histogram & boxplot of residuals]()

  - Q-Q plot: Residuals closely follow the normal line with a slight deviation in the upper tail, which is acceptable.

Overall, the final model met the linear regression assumptions and its results (coefficients, p-values) can be trusted for inference.

- **Most Impactful Predictors**:

![Tornado Diagram]() 

  - The interaction between income and house value had the largest impact.
  - The most impactful predictors of poverty rates are “median house value” and “median household income” as they both show strong negative relationships. Counties with higher home values and incomes tend to have lower poverty rates.
  - Other variables had smaller coefficients but still measurable effects.
    - Higher unemployment associates with higher poverty
    - Greater health insurance coverage comes with lower poverty
    - More public transit use relates to higher poverty (possibly reflecting urban conditions)


Counties with higher incomes and home values tend to have significantly lower poverty rates. On the other hand, higher unemployment, greater health insurance coverage and more use of public transit (a potentially tied to urban poverty) were associated with higher poverty.

Surprisingly, public assistance rates and the percentage of bachelor’s degree holders were not statistically significant in the final model. This means that these factors have limited unique contribution to predictive power of the model once other variables were controlled. 

It is important to note that unlike SPM, the OPM does not include non-cash public assistance (like SNAP, housing subsidies, TANF) in its calculation. So counties with high assistance rates may not show reduced poverty under OPM even though aid might be helping in reality.

## Recommended Courses of Action
A local government or policymaker could use this model to identify counties most at risk based on these factors and effectively target resources or policies.
- Invest in income growth and housing affordability: These were the strongest predictors of lower poverty. Policies targeting wage growth, job access, and affordable housing could significantly reduce poverty rates.
- Expand access to health insurance: Health insurance coverage was significantly linked to lower poverty. Improving coverage could reduce financial hardship and support poverty reduction efforts.

## Final Thoughts

This project demonstrates how careful data wrangling, transparent statistical methods, and principled diagnostics can produce models that are both insightful and trustworthy. It also highlights the importance of questioning assumptions, especially when working with policy-related data.

Not every result was expected. Public assistance didn’t come through as a statistically significant predictor — likely due to limitations of the Official Poverty Measure (OPM), which does not account for non-cash assistance like SNAP or housing vouchers. That’s a structural flaw in the poverty definition itself — not necessarily in the data.

This is a reminder: statistics model relationships, not realities. The real world is messier. Numbers don’t capture dignity, barriers, or the trade-offs that people in poverty navigate every day.

Still, we can quantify strong patterns. And we should, especially when it helps decision-makers focus investments in education, income support, housing, and healthcare — where they’ll make the most impact.

If you're a policymaker, nonprofit leader, or fellow data scientist: I hope this analysis adds value to your work or sparks new questions worth pursuing.

