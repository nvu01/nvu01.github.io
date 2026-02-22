---
layout: post
title: "Undervalued Stock Scanner 2.0: From Spreadsheet Automation to Scalable Python Pipelines"
description: >
  This project rebuilds a spreadsheet-based stock screener into scalable Python ETL pipelines that applies financial logic and statistical methods to detect undervalued opportunities and monitor exit signals.
image: /assets/img/posts/6/Untitled design 2.jpg
tags: [python, dashboard, stock market, financial market]
---
This new version of Undervalued Stock Scanner is a complete architectural shift from my original system. What began as financial spreadsheet modeling has evolved into modular Python pipelines that automate data ingestion, statistical processing, valuation screening, and exit monitoring.

<a href="https://github.com/nvu01/Undervalued-Stock-Scanner-2.0" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo
</a>

**Disclaimer: This project is for educational purposes only. The analysis, models, and methods used here are not financial advice. Investing carries risk, and any decisions based on this analysis are your responsibility. Always do your own research or consult with a qualified financial advisor before making investment decisions.**

* toc
{:toc .large-only}

## Why Rebuild It?

The original <a href="https://nvu01.github.io/featured_projects/2025-06-15-undervalued-stock-scanner/" target="_blank" rel="noopener">Undervalued Stock Scanner</a> was built using Excel, Power Query, and VBA. Excel is powerful. Power Query is flexible. VBA automates well within its environment. Everything worked well for structured analysis and dashboarding, but data processing was tied to a desktop workflow: manual refreshes, layered query dependencies, and logic embedded inside spreadsheet environments.

As a data analyst who’s always looking to streamline processes, I’m constantly searching for ways to make data workflows cleaner, more efficient, and easier to maintain. For this project, I wanted a more robust data processing method that offers:

- A clear separation between data processing and presentation
- Reproducible pipelines independent of UI tools
- Modular scripts instead of layered query chains
- Better statistical handling of outliers
- A system that could scale without becoming fragile

So I rebuilt the entire system in Python, all outside the constraints of Excel.


## Re-Engineering the Pipeline

Instead of relying on workbook refresh cycles, the new system uses Python scripts that:
- Process raw sector CSV files and applies valuation logic
- Monitor held positions for red flags
- Generate on-demand fundamental snapshots

Raw sector CSV exports are placed into predefined input folders. From there, the scripts automatically retrieve all relevant files, process them in batch, apply screening and statistical logic, and export Excel outputs into designated destination folders. Those outputs then serve as clean, structured data sources for the Power BI dashboards.

The process becomes: Drop files in → Run the scripts → Clean outputs generated → Refresh dashboard.

The scripts use Python’s *os* and *glob* libraries to automatically locate and retrieve all relevant files and export structured outputs into designated destination folders. The system maintains consistent naming conventions and directory organization. This design reduces manual error, improves reproducibility, and makes the workflow significantly easier to scale across sectors.

Most importantly, calculation logic is now explicit and centralized in code rather than distributed across interconnected spreadsheet formulas.


## Conceptual Framework Summary

The scanner evaluates key fundamentals like P/FCF, P/B, P/E, ROE, ROA, and A/E. To make comparisons fair, it assesses stocks relative to industry peers in the same market cap groups rather than across the entire market. Outliers are filtered using quartile bounds, and z-scores standardize each metric to allow consistent comparison between stocks.

A stock passes the preliminary scan only if it meets all baseline conditions. Stocks that pass are then ranked using bonus signals.

A small change in business logic: REITs in the Real Estate sector are excluded. Metrics like AFFO, NAV, and NOI are more appropriate for evaluating REITs, but gathering and processing these specialized metrics would require additional resources. For now, the scanner focuses on non-REIT companies, where standard fundamentals are meaningful and comparable.

One of the biggest upgrades is the Exit Signals Framework. The original project only identified undervalued stocks. Now, it also flags overvaluation, quality deterioration, and severe financial red flags for held positions. These are review triggers, not automatic sell signals. My goal was to design a system that helps me manage the full lifecycle of an investment decision.

For a deeper dive into the original methodology and screening logic, see <a href="https://nvu01.github.io/featured_projects/2025-06-15-undervalued-stock-scanner/#what-makes-a-stock-undervalued" target="_blank" rel="noopener">What Makes a Stock Undervalued?</a>


## Explore the Dashboards

Below are the interactive dashboards that bring this system to life.

#### Undervalued Stock Scanner Dashboard

👉 <a href="https://app.fabric.microsoft.com/view?r=eyJrIjoiZjMyNWFiOTQtZTdjYy00MDExLWEzNWUtYzYxODllZDY1MGI3IiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9" target="_blank" rel="noopener">Open the dashboard in new tab</a>.

<iframe title="Undervalued Stock Scanner" style="width: 100%; height: 60vh;" src="https://app.fabric.microsoft.com/view?r=eyJrIjoiZjMyNWFiOTQtZTdjYy00MDExLWEzNWUtYzYxODllZDY1MGI3IiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9" frameborder="0" allowfullscreen="true" ></iframe>

>In this version, I added a drill-through page that allows users to right-click on any stock and navigate to a detailed profile view. This page displays all available fundamentals for the selected company, including its full company name, valuation and scoring signals. To bridge analytics with real-world research, the drill-through page also includes a direct link to the company’s profile on Yahoo Finance.
{:.lead}

#### Exit Signals Dashboard

👉 <a href="https://app.fabric.microsoft.com/view?r=eyJrIjoiYzI4MWZmMGYtZTYwNy00MmNjLWI3NDUtZWRlOWM5ZGFhY2U0IiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9" target="_blank" rel="noopener">Open the dashboard in new tab</a>.

<iframe title="Exit Signals" style="width: 100%; height: 60vh;" src="https://app.fabric.microsoft.com/view?r=eyJrIjoiYzI4MWZmMGYtZTYwNy00MmNjLWI3NDUtZWRlOWM5ZGFhY2U0IiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9" frameborder="0" allowfullscreen="true" ></iframe>

>The Exit Signals dashboard uses conditional formatting to highlight valuation and quality signals that classify stocks into red flag types. Its simple layout, combined with dynamic filtering, allows for focused risk review.
{:.lead}


## Final Reflection

Rebuilding this project required more than a language change from Excel formulas and Power Query M to Python. It challenged me to rethink where logic should live, how data should flow, how automation should scale, and how analytics should be engineered. 

It also meant moving on from a system I had invested significant time and effort building. The original Excel, Power Query, and VBA framework worked, and I was proud of it. But improvement sometimes requires letting go of what already works in order to build something more robust. The rebuilt system reflects how I approach data and workflow challenges. I actively look for ways to streamline processes, even when that means redesigning them from the ground up. For me, improving systems isn't about chasing new tools; it is about prioritizing accuracy, consistency, and long-term maintainability.


## 🔗 Related Projects

### Undervalued Stock Trade Tracking

I also built an Undervalued Stock Trade Tracking system that automates the entire process of tracking and analyzing trade history of the Undervalued Stock strategy. Its Python-based ETL pipeline automatically accesses the file system to locate and retrieve the latest Thinkorswim statements, processes new trade history, and updates a clean dataset used for real-time Excel reporting.

Feel free to check it out for more details on how I handle trade history, ETL, and real-time Excel reporting.

👉 <a href="https://nvu01.github.io/other_projects/#-undervalued-stock-trade-tracking" target="_blank" rel="noopener">See Undervalued Stock Trade Tracking</a>


### Undervalued Stock Scanner 1.0

The original Undervalued Stock Scanner used Excel, Power Query, VBA and Power BI to screen stocks based on financial valuation rules. It established the framework later rebuilt into the new version 2.0.

Explore it to learn more about the original concepts and legacy pipeline.

👉 <a href="https://nvu01.github.io/featured_projects/2025-06-15-undervalued-stock-scanner/" target="_blank" rel="noopener">See Original Undervalued Stock Scanner</a>