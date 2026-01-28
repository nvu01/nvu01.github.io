---
# Featured tags need to have either the `list` or `grid` layout (PRO only).
layout: page

# The title of the tag's page.
title: Other Projects

# The name of the tag, used in a post's front matter (e.g. tags: [<slug>]).
slug: other_projects

# (Optional) Write a short (~150 characters) description of this featured tag.
description: >
  Here are some of the projects I’ve worked on that aren't covered in my blog posts. You can find the code and more details in the GitHub repositories.
  
# (Optional) Hide the description
hide_description: true

# (Optional) You can disable grouping posts by date.
# no_groups: true

# Exclude this example category from the sitemap.
# DON'T USE THIS SETTING IN YOUR CATEGORIES!
sitemap: false

permalink: /other_projects/
---

Here are some of the projects I’ve worked on that aren't covered in my blog posts. You can find the code and more details in the GitHub repositories.

* toc
{:toc .large-only}

---

## 📌 ETL Pipeline & Data Modeling for Music Streaming Data

This project focuses on building an ETL pipeline and designing a star schema for analyzing song play data. Using Python and SQL, data is extracted from JSON-formatted song and user activity logs, transformed, and loaded into a PostgreSQL database structured with one fact table and multiple dimension tables. The resulting schema supports efficient querying of song play events for the fictional music streaming service Sparkify. The pipeline can be executed via scripts or notebooks, and includes data validation to ensure accuracy.

<a href="https://github.com/nvu01/ETL-Pipeline-and-Data-Modeling" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>


| **Tools:**                | Jupyter Notebook, PostgreSQL |
| **Language:**             | Python, SQL                  |
| **Frameworks/Libraries:** | psycopg2, pandas, os & glob  |


**Skills:**
- **Data modeling**: Designing and implementing a star schema with fact and dimension tables.
- **ETL development**: Building an Extract, Transform, Load pipeline for structured data ingestion.
- **SQL & relational databases**: Writing SQL queries for table creation, data insertion, and validation in PostgreSQL.
- **Python scripting**: Automating data processing and database interaction using Python scripts.
- **Data cleaning & transformation**: Processing raw JSON files to extract relevant information.
- **Testing & validation**: Verifying data integrity through queries and checks in notebooks

---

## 📌 Supervised Learning: Predicting Donors for CharityML

This project applies supervised machine learning to U.S. census data to help the fictional non-profit CharityML identify potential donors. Using Python and scikit-learn, I preprocessed and transformed the raw data, evaluated and compared multiple classifiers, including **Random Forest**, **AdaBoost**, and **Logistic Regression**. I selected the best-performing model through cross-validation and optimization. I also investigated model performance, feature importance, and algorithm trade-offs to support business decisions.

<a href="https://github.com/nvu01/Supervised-Learning" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>


| **Tools:**                | Jupyter Notebook                        |
| **Language:**             | Python                                  |
| **Frameworks/Libraries:** | pandas, NumPy, scikit-learn, matplotlib |


**Skills:**
- **Supervised learning**: Training and comparing classification models to identify optimal performance.
- **Data preprocessing**: Cleaning, transforming, and encoding categorical census data.
- **Model evaluation**: Using accuracy, precision, recall, and F-beta score to benchmark models.
- **Hyperparameter tuning**: Optimizing selected models via grid search and cross-validation.
- **Feature importance analysis**: Interpreting model predictions and understanding key drivers of donor likelihood.
- **Python scripting**: Writing modular, reusable code for reproducible ML pipelines.

---

## 📌 Unsupervised Learning: Customer Segmentation with PCA & K-Means Clustering

In this project, I performed unsupervised learning to identify distinct customer segments for a German mail-order company using large-scale demographic data. The pipeline includes extensive preprocessing, feature transformation with PCA, and customer segmentation using K-means clustering. The final analysis compares customer groups to the general population, revealing patterns in consumer behavior that support targeted marketing strategies.

<a href="https://github.com/nvu01/Unsupervised-Learning" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>

| **Tools:**                | Jupyter Notebook                        |
| **Language:**             | Python                                  |
| **Frameworks/Libraries:** | pandas, NumPy, scikit-learn, matplotlib |

**Skills:** 
- **Unsupervised learning**: Applied K-means clustering to uncover latent segments within high-dimensional demographic data.
- **Dimensionality reduction**: Used PCA to visualize structure, reduce noise, and streamline clustering performance.
- **Data preprocessing**: Addressed extensive missing and encoded values, and scaled features for consistency.
- **Customer analysis**: Mapped clusters from general population data to customer records to highlight key consumer profiles.
- **Scalable analysis**: Created a repeatable end-to-end process for transforming, reducing, and clustering large datasets with nearly a million entries and 85 features.

---

## 📌 SQLite Database for Weather Data

This project involves building a Python program to retrieve and store historical weather data from the Open Meteo API for specific locations and dates within the past five years. The program collects key weather metrics such as mean temperature, maximum wind speed, and total precipitation for each year and aggregates them. The data is stored in a local SQLite database (my_database.db), and the program offers functions to add, query, and delete records from this database. Additionally, the project includes unit test to check the functionality of the core components.

<a href="https://github.com/nvu01/SQLite-Database-for-Weather-Data" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>


| **Tools:**                | PyCharm, SQLite, Open Meteo API |
| **Language:**             | Python                          |
| **Frameworks/Libraries:** | SQLAlchemy, unittest            |


**Skills:**
- **API integration**: Consuming and integrating external APIs to retrieve weather data.
- **Database management**: Creating, modifying, and querying a SQLite database.
- **Data aggregation**: Aggregating and processing weather data across multiple years.
- **Python scripting**: Writing Python scripts to interact with APIs and databases.
- **Unit testing**: Writing and running tests using the unittest framework.

---

## 📌 A/B Test Analysis for E-Commerce Conversion Optimization

This project analyzes the results of an A/B test run by an e-commerce company to evaluate whether a new webpage version improves user conversion. Using Python and statistical modeling, I conducted an end-to-end analysis covering descriptive statistics, hypothesis testing, and regression analysis to determine whether the new design should be implemented.

<a href="https://github.com/nvu01/AB-Test-Analysis" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>


| **Tools:**                | Jupyter Notebook                                                    |
| **Language:**             | Python                                                              |
| **Frameworks/Libraries:** | pandas, NumPy, scikit-learn, matplotlib, seaborn, statmodels, scipy |


**Skills:**
- **A/B testing**: Designed and interpreted an A/B test using bootstrapping and p-value analysis.
- **Hypothesis testing**: Simulated control/treatment outcomes to assess statistical significance of conversion differences.
- **Logistic regression modeling**: Built and interpreted a logistic model to analyze the impact of page version and country on conversion.
- **Data wrangling & validation**: Verified group assignments and cleaned mismatched records to ensure experiment integrity.
- **Insight communication**: Presented evidence-based recommendations about whether to deploy the new page or conduct further testing.

---

## 📌 Undervalued Stock Trade Tracking

This project automates the tracking and analysis of undervalued stock trades using a Python-based ETL pipeline integrated with Power Query and Excel for real-time reporting. The system retrieves monthly account and position statements exported from Thinkorswim, extracts relevant trading activity from CSV files, processes new undervalued trades, and updates a historical dataset used for portfolio analysis. The final Excel report incorporates live market data and visualizations to provide an up-to-date view of performance and portfolio composition.

<a href="https://github.com/nvu01/Undervalued-Stock-Trade-Tracking" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>

| **Tools:**                | Jupyter Notebook, VSCode, Excel, Power Query |
| **Language:**             | Python, VBA                                  |
| **Frameworks/Libraries:** | pandas, glob, os, io, argparse               |

**Skills:**
- **ETL development**: Automating monthly extraction, transformation, and loading of trade and position data using file-system logic and custom Python functions.
- **Data manipulation (datetime-heavy)**: Converting and aligning timestamps, filtering trade history, and performing time-based merges between datasets.
- **Excel reporting**: Building dynamic reports with real-time stock prices, treemaps, and waterfall charts.
- **Financial analysis**: Generating performance metrics such as ROI, P&L, investment totals, and portfolio weight.
- **Applying best practices for data confidentiality**: Protecting personal and financial information by masking and concealing sensitive data before publishing or sharing.