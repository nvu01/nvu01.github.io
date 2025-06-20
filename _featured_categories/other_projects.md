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

### ETL Pipeline & Data Modeling for Music Streaming Data

This project focuses on building an ETL pipeline and designing a star schema for analyzing song play data. Using Python and SQL, data is extracted from JSON-formatted song and user activity logs, transformed, and loaded into a PostgreSQL database structured with one fact table and multiple dimension tables. The resulting schema supports efficient querying of song play events for the fictional music streaming service Sparkify. The pipeline can be executed via scripts or notebooks, and includes data validation to ensure accuracy.

<a href="https://github.com/nvu01/ETL-Pipeline-and-Data-Modeling" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>


| **Tools**        | **Language** | **Frameworks/Libraries** |
|------------------|--------------|--------------------------|
| Jupyter Notebook | Python       | psycopg2                 |
| PostgreSQL       | SQl          | pandas                   |
|                  |              | os & glob                |

**Skills:**
- **Data Modeling**: Designing and implementing a star schema with fact and dimension tables.
- **ETL Development**: Building an Extract, Transform, Load pipeline for structured data ingestion.
- **SQL & Relational Databases**: Writing SQL queries for table creation, data insertion, and validation in PostgreSQL.
- **Python Scripting**: Automating data processing and database interaction using Python scripts.
- **Data Cleaning & Transformation**: Processing raw JSON files to extract relevant information.
- **Testing & Validation**: Verifying data integrity through queries and checks in notebooks

---

### Supervised Learning: Predicting Donors for CharityML

This project applies supervised machine learning to U.S. census data to help the fictional non-profit CharityML identify potential donors. Using Python and scikit-learn, I preprocessed and transformed the raw data, evaluated and compared multiple classifiers, including **Random Forest**, **AdaBoost**, and **Logistic Regression**. I selected the best-performing model through cross-validation and optimization. I also investigated model performance, feature importance, and algorithm trade-offs to support business decisions.

<a href="https://github.com/nvu01/Supervised-Learning" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>

| **Tools**        | **Language** | **Frameworks/Libraries** |
|------------------|--------------|--------------------------|
| Jupyter Notebook | Python       | pandas                   |
|                  |              | NumPy                    |
|                  |              | scikit-learn             |
|                  |              | matplotlib               |

**Skills:**
- **Supervised Learning**: Training and comparing classification models to identify optimal performance.
- **Data Preprocessing**: Cleaning, transforming, and encoding categorical census data.
- **Model Evaluation**: Using accuracy, precision, recall, and F-beta score to benchmark models.
- **Hyperparameter Tuning**: Optimizing selected models via grid search and cross-validation.
- **Feature Importance Analysis**: Interpreting model predictions and understanding key drivers of donor likelihood.
- **Python Scripting**: Writing modular, reusable code for reproducible ML pipelines.

---

### Unsupervised Learning: Customer Segmentation with PCA & K-Means Clustering

In this project, I performed unsupervised learning to identify distinct customer segments for a German mail-order company using large-scale demographic data. The pipeline includes extensive preprocessing, feature transformation with PCA, and customer segmentation using K-means clustering. The final analysis compares customer groups to the general population, revealing patterns in consumer behavior that support targeted marketing strategies.

<a href="https://github.com/nvu01/Unsupervised-Learning" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>

| **Tools**        | **Language** | **Frameworks/Libraries** |
|------------------|--------------|--------------------------|
| Jupyter Notebook | Python       | pandas                   |
|                  |              | NumPy                    |
|                  |              | scikit-learn             |
|                  |              | matplotlib               |

**Skills:** 
- **Unsupervised Learning**: Applied K-means clustering to uncover latent segments within high-dimensional demographic data.
- **Dimensionality Reduction**: Used PCA to visualize structure, reduce noise, and streamline clustering performance.
- **Data Preprocessing**: Addressed extensive missing and encoded values, and scaled features for consistency.
- **Customer Analysis**: Mapped clusters from general population data to customer records to highlight key consumer profiles.
- **Scalable Analysis**: MDesigned a repeatable end-to-end process for transforming, reducing, and clustering large datasets with nearly a million entries and 85 features.

---

### SQLite Database for Weather Data

This project involves building a Python program to retrieve and store historical weather data from the Open Meteo API for specific locations and dates within the past five years. The program collects key weather metrics such as mean temperature, maximum wind speed, and total precipitation for each year and aggregates them. The data is stored in a local SQLite database (my_database.db), and the program offers functions to add, query, and delete records from this database. Additionally, the project includes unit test to check the functionality of the core components.

<a href="https://github.com/nvu01/SQLite-Database-for-Weather-Data" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo</a>


| **Tools**       | **Language** | **Frameworks/Libraries** |
|-----------------|--------------|--------------------------|
| PyCharm         | Python       | SQLAlchemy               |
| Open Meteo API  |              | unittest                 |
| SQLite          |              |                          |

**Skills:**
- **API Integration**: Consuming and integrating external APIs to retrieve weather data.
- **Database Management**: Creating, modifying, and querying a SQLite database.
- **Data Aggregation**: Aggregating and processing weather data across multiple years.
- **Python Scripting**: Writing Python scripts to interact with APIs and databases.
- **Unit Testing**: Writing and running tests using the unittest framework.








