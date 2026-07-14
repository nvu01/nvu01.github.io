---
layout: post
title: "Undervalued Stock Scanner 2.0: From Spreadsheet Automation to Scalable Python Pipelines"
description: >
  Python (os, glob, pandas, numpy) • Power BI • DAX • Deneb visuals • Power Query • ETL pipeline
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

The original <a href="https://nvu01.github.io/featured_projects/2025-06-15-undervalued-stock-scanner/" target="_blank" rel="noopener">Undervalued Stock Scanner</a> was built using Excel, Power Query, and VBA. I initially chose Excel because I wanted to use the Real-Time Data (RTD) function to stream live stock prices directly from Thinkorswim into my valuation models. At first, this seemed essential as I could get real-time price-related metrics like P/E, P/B, and P/FCF. However, in practice, I review screening results on the same day that I update financial data, during after-hours. Because the analysis is performed after market close, intraday price fluctuations don’t affect my decision-making process. End-of-day pricing is sufficient for how I evaluate screening results.

I continued to use this model for a year because it worked well for structured analysis and dashboarding. Excel was flexible. Power Query handled data transformation well. VBA automated repetitive data refresh tasks. However, data processing was tied to a desktop workflow: fragmented data update across separate sector workbooks, layered query dependencies, and logic embedded inside spreadsheet environments. 

As a data analyst who’s always looking to streamline processes, I’m constantly searching for ways to make data workflows cleaner, more efficient, and easier to maintain. For this project, I wanted a more robust data processing method that offers:

- A clear separation between data processing and presentation
- Reproducible pipelines independent of UI tools
- Modular scripts instead of layered query chains
- Better statistical handling of outliers
- Centralized batch processing across sectors
- A system that could scale without becoming fragile

So I rebuilt the entire system in Python, all outside the constraints of Excel.


## Re-Engineering the Pipeline

Instead of relying on fragmented workbook refresh cycles, the new system uses Python scripts that:
- Batch Processing: Processes raw CSV files and applies valuation logic in bulk.
- Risk Monitoring: Tracks held positions for active financial red flags.
- Historical Storage: Commits monthly stock data to a local SQLite database for time-series trend analysis.

Raw sector CSV exports are placed into predefined input folders. From there, the scripts automatically retrieve all relevant files, process them in batch, apply screening and statistical logic, and export Excel outputs into designated destination folders. Those outputs then serve as clean, structured data sources for the Power BI dashboards.

**The process becomes: Drop files in → Run the scripts → Clean outputs generated → Update SQLite Database → Refresh dashboards.**

This architecture reduces manual error, improves reproducibility, and makes the workflow significantly easier to scale across sectors. Most importantly, calculation logic is now explicit and centralized in code rather than distributed across interconnected spreadsheet formulas.

To further streamline operations, I created .bat files to allow full batch execution with a single click.


## Conceptual Framework Summary

The scanner evaluates key fundamentals like P/FCF, P/B, P/E, ROE, ROA, and A/E. To make comparisons fair, it assesses stocks relative to industry peers in the same market cap groups rather than across the entire market. Outliers are filtered using quartile bounds, and z-scores standardize each metric to allow consistent comparison between stocks.

Stocks must clear all baseline conditions to pass the preliminary scan, after which they are ranked using additional bonus signals.

For a deeper dive into the original methodology and screening logic, see <a href="https://nvu01.github.io/featured_projects/2025-06-15-undervalued-stock-scanner/#what-makes-a-stock-undervalued" target="_blank" rel="noopener">What Makes a Stock Undervalued?</a>

Key Scope & Feature Upgrades:
- Sector Optimization (Excluding REITs): Real Estate Investment Trusts (REITs) are explicitly excluded from the scanner. Evaluating REITs accurately requires specialized metrics like AFFO, NAV, and NOI. Because sourcing this data requires premium resources, the scanner purposefully focuses on non-REIT companies where standard fundamental metrics remain highly meaningful and comparable.
- Exit Signals Framework: While the initial iteration only identified undervalued entries, this upgrade introduces an active monitoring framework. The system flags overvaluation, quality deterioration, and severe financial red flags for existing positions. These act as systematic review triggers rather than automated sell signals.
- Time-Series Analysis: By capturing historical data over time, the system enables diagnostic health checks on individual stocks.

My goal was to design a system that helps me manage the full lifecycle of an investment decision.


## Explore the Dashboards

#### 1. Undervalued Stock Scanner Dashboard

For this scanner version, I added a drill-through page that allows users to right-click on any stock to navigate to a detailed profile view displaying all available information for the selected company: its full company name, valuation metrics and scores. I also added a dynamic link to the company’s profile on Yahoo Finance so I can jump straight from the analysis to real-world research.

Visually, I went with a frosty glass aesthetic to give it a more polished, modern feel. The dashboard uses Deneb visuals, which let me write JSON to fine-tune every aspect of the charts exactly the way I want.

👉 <a href="https://app.fabric.microsoft.com/view?r=eyJrIjoiZjMyNWFiOTQtZTdjYy00MDExLWEzNWUtYzYxODllZDY1MGI3IiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9" target="_blank" rel="noopener">Open the dashboard in new tab</a>.

<iframe 
  title="Undervalued Stock Scanner" 
  src="https://app.fabric.microsoft.com/view?r=eyJrIjoiZjMyNWFiOTQtZTdjYy00MDExLWEzNWUtYzYxODllZDY1MGI3IiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9"
  style="
    width: 1280px;
    height: 780px;
    transform: scale(0.65);
    transform-origin: 0 0;
    margin-bottom: -240px;
    border: none;
    display: block;
  "
  frameborder="0"
  allowfullscreen="true">
</iframe>

#### 2. Stock Monitor Dashboard

**Exit Signals View**: Employs precise conditional formatting to categorize and highlight specific risk types, utilizing dynamic filters for rapid portfolio health reviews.

**Trend Analysis View**: Surfaces interactive time-series charts for every tracked metric, making it easy to isolate and analyze historical performance trajectories for any chosen ticker.

👉 <a href="https://app.fabric.microsoft.com/view?r=eyJrIjoiYzI4MWZmMGYtZTYwNy00MmNjLWI3NDUtZWRlOWM5ZGFhY2U0IiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9" target="_blank" rel="noopener">Open the dashboard in new tab</a>.

<iframe title="Stock Monitor" style="width: 100%; height: 56vh;" src="https://app.fabric.microsoft.com/view?r=eyJrIjoiOGFiYTkwNjAtMjU3NS00YmNkLWI0OTEtMzI2NDFlNmFkNzMxIiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9" frameborder="0" allowfullscreen="true" ></iframe>

Note: Some data in the dashboard's data source was masked and concealed to ensure personal and financial information security. Hence, the dashboard does not reflect my real portfolio holdings.

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