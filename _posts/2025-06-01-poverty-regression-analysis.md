---
layout: post
title: Socioeconomic Factors Impacting Poverty in U.S. Counties
description: >
  A regression-based analysis of how socioeconomic variables drive poverty rates across 854 U.S. counties, using data from the U.S. Census Bureau.
image: /assets/img/blog/poverty-tornado-diagram.png
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

## Data Wrangling

Data from ACS tables were saved as .json files, parsed using Python, and combined into a single county-level dataset with Pandas. During data preparation, I renamed coded headers to descriptive variable names, converted data types, and addressed missing or special values by imputing based on 2022 ACS data. I also removed redundant columns and combined related variables to enhance usability. The cleaned dataset was then saved as a .csv file for modeling.

## Summary of Data Analysis Methods

I began EDA with descriptive statistics to examine central tendencies and spread. This is followed by calculating a correlation matrix and VIF to detect multicolinearity. I dropped or transformed any predictor whose VIF topped 5. To explore relationships between the response and explanatory variables, I used pairplots and scatter plots. To address nonlinearity and skewness in the data, I applied appropriate transformations based on the distribution and each variable's relationship with the response: log transformation for heavy right-tails, log1p when zeros appeared, and square-root for moderate skew.

The main analytical approach was a multiple linear regression method, which allowed me to quantify relationships between socioeconomic factors and poverty rates while considering the influence of multiple variables simultaneously. Specifically, the project used ordinary least squares (OLS) model which allowed a straightforward interpretation of coefficients, significance testing and model evaluation.

To evaluate the model’s predictive performance, I used metrics such as R-squared on both the training and test sets, adjusted R-squared, and mean squared error (MSE) on the test set. These metrics provided insight into how well the model fit the training data and how accurately it predicted poverty rates on new, unseen data.

To evaluate the role of socioeconomic factors in explaining poverty rates across U.S. counties, both a global and individual hypothesis testing framework will be used.
- Global hypothesis (F-test): This test evaluates whether the full set of predictors contributes to explaining poverty rates.
  - Null hypothesis: All regression coefficients are equal to zero  
    𝐻0: 𝛽1=𝛽2=⋯=𝛽𝑘=0
  - Alternative hypothesis: At least one regression coefficient is not equal to zero  
    𝐻1: 𝐴𝑡 𝑙𝑒𝑎𝑠𝑡 𝑜𝑛𝑒 𝛽𝑖≠0
- Individual hypotheses (t-test for each coefficient): These tests assess the significance of each predictor.
	- Null Hypothesis: The coefficient for predictor i is zero.  
    H0: βi=0
	- Alternative Hypothesis: The coefficient for predictor i is not zero.  
    H1: βi≠0

To evaluate the relative importance of each socioeconomic factor in explaining poverty rates, I also used the standardized coefficients from the multiple linear regression model. These coefficients were obtained by scaling all independent variables using MinMaxScaler before fitting the model. This will ensure that the predictors are on the same scale.

For the baseline model and the improved model, I implemented residual analysis to verify model assumptions and ensure the model’s validity. OLS regression relies on several assumptions: linearity of relationships between predictors and the dependent variable, homoscedasticity (constant variance of residuals), independence of residuals, and normally distributed errors. The analysis included visualizations such as residual plots, histogram and boxplot of residuals, and Q-Q plot. This diagnostic step helped confirm whether the use of OLS and the resulting hypothesis tests were valid.

Finally, to address issues identified in model diagnostics, I applied several refinement methods. The response variable was transformed to reduce heteroscedasticity and improve linearity. An interaction term was added to improve model accuracy when the effect of one variable depends on another. Robust standard errors (HC3) were used to produce more reliable p-values in the presence of heteroscedasticity.

## Project Outcomes

- **Predictive Power**: My refined regression model worked well and explained 79.6% of the variance in training data and 83.1% in the test set. That’s high, especially for social data, where perfect predictions are rare. 

- **Overall Model Significance:** Based on the F-test result, the final model was statistically significant overall (p < 0.001).

- **Model Validity:** 
  - Residual vs fitted plot: Residuals are randomly scattered around zero with consistent spread across fitted values. This means there is no major heteroscedasticity. A few mild outliers are present.
  - Residuals vs predictors: No strong patterns or funnel shapes. This supports the assumption of constant variance and linearity across predictors.
  - Histogram & boxplot of residuals: Distribution is roughly normal, bell-shaped, and symmetrical. The median is near zero, with a few mild upper-end outliers.
  - Q-Q plot: Residuals closely follow the normal line with a slight deviation in the upper tail, which is acceptable.

Overall, the final model met the linear regression assumptions and its results (coefficients, p-values) can be trusted for inference.

- **Most Impactful Predictors**:
  - **Interaction between income and home value**
  - **Median household income** (log-transformed)
  - **Median home value** (square root-transformed)
  - **Health insurance coverage**
  - **Public transit usage** (log-transformed)

Counties with higher incomes and home values tend to have significantly lower poverty rates. On the other hand, higher unemployment, greater health insurance coverage and more use of public transit (a potentially tied to urban poverty) were associated with higher poverty.

Surprisingly, public assistance rates and the percentage of bachelor’s degree holders were not statistically significant in the final model. This means that these factors have limited unique contribution to predictive power of the model once other variables were controlled.

