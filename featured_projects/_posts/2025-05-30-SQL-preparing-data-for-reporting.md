---
layout: post
title: "Preparing Data for Reporting Using PostgreSQL"
description: >
  This project uses PostgreSQL and PL/pgSQL to extract, transform and organize DVD rental data to support future business reporting. It demonstrates skills in SQL functions, triggers, and stored procedures.
image: /assets/img/posts/2/PostgreSQL.png
tags: [Waggle, Power BI report, data visualization, storytelling, LapDog, LapCat]
---

This project demonstrates how SQL and PostgreSQL can be used to transform raw transactional data into structured, analysis-ready tables. Using the DVD Rental Dataset, I built a structured workflow to extract, transform, and organize rental data for future insights and analysis.

<a href="https://github.com/nvu01/Advanced-Data-Management" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo
</a>

* toc
{:toc .large-only}

## Project Overview

### Database

**Sample Database:** dvdrental.zip containing the database is available for download in my [GitHub repo](https://github.com/nvu01/Advanced-Data-Management)
or from [neon.tech](https://neon.tech/postgresql/postgresql-getting-started/postgresql-sample-database)

**Data Model (ERD):** <a href="/assets/img/posts/2/dvdrental_data_model.png" target="_blank">View data model</a>

**Source Tables Used:** I used two key tables from the DVD Rental sample database:

- `rental`: Contains information about each film rental.

|Column Name|Data Type                |
|-----------|---------------------------|
|rental_id  |integer                    |
|rental_date|timestamp without time zone|
|inventory_id|integer                   |
|customer_id|smallint                   |
|return_date|timestamp without time zone|
|staff_id   |smallint                   |
|last_update|timestamp without time zone|

- `category`: Provides the category_name for each film.

|Column Name|Data Type                  |
|-----------|---------------------------|
|category_id|integer                    |
|name       |character varying          |
|last_update|timestamp without time zone|

**Tables Created:**

- `detailed_table`: A transactional table showing individual rental records with added time and category context.

|Column Name  |Data Type                  |
|-------------|---------------------------|
|rental_id    |integer                    |
|rental_year  |integer                    |
|rental_month |integer                    |
|category_name|character varying          |

- `summary_table`: An aggregated table used for reporting the total number of rentals by genre per month.

|Column Name  |Data Type                  |
|-------------|---------------------------|
|rental_year  |integer                    |
|rental_month |integer                    |
|category_name|character varying          |
|num_rentals  |bigint                     |

### Business Use Cases

**detailed_table:**
- Useful for looking up individual rental instances by date and genre.
- Helps analysts or support staff answer questions like:
  - “What genre was rented on a specific date?”
  - “How many horror movies were rented in a specific rental instance?”

**summary_table:**
- Supports trend and performance analysis across months.
- Helps stakeholders understand:
  - Which genres are most popular over time
  - Seasonal rental trends
  - How genre preferences shift month-to-month

The data is designed to be refreshed monthly, ensuring that reporting and insights remain current for ongoing business needs.

### Deliverables

- Create reusable **user-defined functions** to extract year and month from timestamps.
- Build **detailed and summary tables** to structure rental data by film category and time.
- Implement a **trigger function** to auto-update summary metrics when new data is inserted.
- Use a **stored procedure** to fully refresh both tables on a monthly basis.

### Tools & Skills Used

**Tools:** PostgreSQL

**Skills:**
- PL/pgSQL scripting
- Data transformation (timestamp extraction)
- Joins & subqueries
- Table creation & triggers
- Stored procedures
- Workflow automation using pgAgent (PostgreSQL's job scheduler)

## Key SQL Components

<a href="https://github.com/nvu01/Advanced-Data-Management/blob/main/dvdrental%20project.sql" target="_blank">View full SQL script</a>

### Extracting Year and Month with Functions

I began by creating two user-defined functions to extract month and year from `rental_date` column in `rental` table.

```sql
-- Create a function that extracts month from the rental_date column
CREATE OR REPLACE FUNCTION rental_month (rental_date timestamp without time zone)
RETURNS int
LANGUAGE plpgsql
AS $$
DECLARE month_value int;
BEGIN
    SELECT EXTRACT (MONTH FROM rental_date) INTO month_value;
    RETURN month_value;
END; 
$$;

-- Create a function that extracts year from the rental_date column
CREATE OR REPLACE FUNCTION rental_year (rental_date timestamp without time zone)
RETURNS int
LANGUAGE plpgsql
AS $$
DECLARE year_value int;
BEGIN
    SELECT EXTRACT (YEAR FROM rental_date) INTO year_value;
    RETURN year_value;
END;
$$;
```


### Creating Tables

Next, I created `detailed_table` and `summary_table`.

```sql
-- Create an empty detailed table
DROP TABLE IF EXISTS detailed_table;
CREATE TABLE detailed_table (
	rental_id int,
	rental_year int,
	rental_month int,
	category_name varchar (25)
);

-- Create a summary table that extracts and aggregates data from the detailed table
DROP TABLE IF EXISTS summary_table;
CREATE TABLE summary_table
AS SELECT rental_year, rental_month, category_name, COUNT(*) AS num_rentals
FROM detailed_table
GROUP BY rental_year, rental_month, category_name
ORDER BY rental_year DESC, rental_month DESC, num_rentals DESC;
```


### Trigger for Summary Table Updates

Once the two tables were created, I could build a trigger that updates the `summary_table` when data is inserted into the `detailed_table`.

```sql
-- Create a function that updates the summary table
CREATE OR REPLACE FUNCTION summary_table_update()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $$
BEGIN
	TRUNCATE summary_table;
	INSERT INTO summary_table
		SELECT rental_year, rental_month, category_name, COUNT (*) AS num_rentals
		FROM detailed_table
		GROUP BY rental_year, rental_month, category_name
		ORDER BY rental_year DESC, rental_month DESC, num_rentals DESC;
RETURN NEW;
END; 
$$;

-- Create a trigger that updates the summary table when data is inserted into the detailed table
DROP TRIGGER IF EXISTS update_summary_on_insert ON detailed_table;
CREATE TRIGGER update_summary_on_insert
AFTER INSERT
ON detailed_table
FOR EACH STATEMENT
EXECUTE PROCEDURE summary_table_update();
```


### Populating Tables

Raw data was then extracted and inserted into the `detailed_table`. This would also trigger update to `summary_table`.

```sql
-- Add raw data to the detailed table
INSERT INTO detailed_table
SELECT r.rental_id, rental_year (r.rental_date), rental_month (r.rental_date), c.name AS category_name
FROM rental r
INNER JOIN inventory i ON r.inventory_id = i.inventory_id
INNER JOIN film_category fc ON i.film_id = fc.film_id
INNER JOIN category c ON fc.category_id = c.category_id
ORDER BY rental_year DESC, rental_month DESC;
```


### Stored Procedure to Refresh All Data

Finally, I created a procedure that refreshes data in both detailed and summary tables.

```sql
-- Create a procedure that re-populates the 2 tables with raw data from the database
-- Any test data that was manually inserted to the detailed table won't be included
DROP PROCEDURE IF EXISTS refresh_tables();
CREATE PROCEDURE refresh_tables ()
LANGUAGE plpgsql
AS $$
BEGIN
	TRUNCATE detailed_table;
	TRUNCATE summary_table;
	-- Temporarily disable trigger
    ALTER TABLE detailed_table DISABLE TRIGGER update_summary_on_insert;
	-- Update detailed_table
	INSERT INTO detailed_table
		SELECT r.rental_id, rental_year (ym.rental_date), rental_month (ym.rental_date), c.name AS category_name
		FROM rental r
		INNER JOIN inventory i ON r.inventory_id = i.inventory_id
		INNER JOIN film_category fc ON i.film_id = fc.film_id
		INNER JOIN category c ON fc.category_id = c.category_id
		INNER JOIN rental ym ON r.rental_id = ym.rental_id
		ORDER BY rental_year DESC, rental_month DESC;
	-- Update summary_table
	INSERT INTO summary_table
		SELECT rental_year, rental_month, category_name, COUNT(*) AS num_rentals
		FROM detailed_table
		GROUP BY rental_year, rental_month, category_name
		ORDER BY rental_year DESC, rental_month DESC, num_rentals DESC;
	-- Re-enable trigger
    ALTER TABLE detailed_table ENABLE TRIGGER update_summary_on_insert;
END;
$$;
```


## Automation with pgAgent

To keep the data fresh for reporting, the stored procedure can be scheduled to run monthly using pgAgent, PostgreSQL’s built-in job scheduler. This ensures the summary reflects the most recent rental data without manual intervention. 


## Final Thoughts

This project highlights the power of SQL and PostgreSQL for preparing data in a way that supports scalable and automated business intelligence workflows. By creating a clean, transformed layer of data ready for analysis, I can bridge the gap between raw transactions and valuable insights. These structured tables can now be easily integrated with tools like Power BI or Tableau for dashboarding, trend analysis, and storytelling with data.