---
layout: post
title: "Undervalued Stock Scanner: From Raw Data to Smart Insights"
description: >
  A collaborative project that combines financial logic with automated Excel and Power BI tools to transform raw data into user-friendly and insight-driven dashboards.
image: /assets/img/posts/2/adam-smigielski-K5mPtONmpHM-unsplash.jpg
tags: [dashboard, stock market, financial market]
---

Like many aspiring investors, my husband and I were drawn to the challenge of identifying undervalued stocks because they are like hidden gems with solid fundamentals that the market hasn't caught up with yet. What started as a weekend project in Excel became a fully automated pipeline combining Power Query, VBA, and Power BI dashboards. 

<a href="https://github.com/nvu01/Undervalued-Stock-Scanner" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo
</a>

**Disclaimer: This project is for educational purposes only. The analysis, models, and methods used here are not financial advice. Investing carries risk. Always do your own research or consult with a financial advisor before making investment decisions.**

* toc
{:toc .large-only}

## Project at a Glance

The idea started with my husband’s interest in value investing and my curiosity for building smarter, faster workflows. He defined the investment logic and I built the engine. Our goal? Identifying potentially undervalued stocks by analyzing key financial metrics across various sectors. The project focuses on three market cap categories (Large Cap, Mid Cap, and Small Cap) and applies statistical methods to assess stock fundamentals.


## Datasets

We used 11 raw CSV files exported from Thinkorswim, each representing a different sector. These contain financial fundamentals segmented by market cap:

- Large-Cap: $10B+
- Mid-Cap: $2B–$10B
- Small-Cap: $250M–$2B

Each sector includes multiple industries. When comparing stocks, it's important to consider market capitalization and industry because a “good” metric in one industry or market cap can be a red flag in another. We structured the pipeline to retain this nuance throughout the analysis.

## What Makes a Stock Undervalued?

### Key Fundamentals

Here’s a quick overview of the financial metrics we used:

#### Price-to-Free Cash Flow ratio (P/FCF)
Price-to-Free Cash Flow (P/FCF): A high P/FCF ratio indicates that the specific firm is trading at a high price but is not generating enough free cash flows to justify the price. Smaller price ratios are generally preferred, as they may reveal a firm generating ample cash flows that may not yet be reflected in the price.
#### Price-to-Book ratio (P/B)
Book Value Per Share (BVPS) shows a company's net assets per share. If BVPS is higher than the stock price, the stock may be undervalued. The P/B ratio compares market price to book value. Thus, P/B of 1 means it is traded at exactly where it should be. Higher P/B means it might be overvalued.
#### Return on Equity (ROE)
This ratio is a gauge of a corporation's profitability and how efficiently it generates those profits. The higher the ROE, the better a company is at converting its equity financing into profits.
#### Return on Assets (ROA)
Return on assets measures how effective a company's management is in generating profit from the total assets on its balance sheet. A ROA that rises over time indicates that the company is doing well at increasing its profits with each investment dollar it spends.
#### Asset-to-equity ratio (A/E)
The asset-to-equity ratio measures a company's financial leverage by comparing its total assets to its shareholders' equity. A higher ratio means more debt and higher financial risk. A lower ratio signals a more conservative, equity-heavy structure. 
#### Price-to-Earnings ratio (P/E)
This metric shows how much investors are paying for each dollar of earnings. A high P/E can signal high growth expectations or overvaluation. A low P/E might suggest undervaluation or strong recent performance.

### How We Evaluate Stocks Using These Metrics
Our evaluation is based on a series of carefully selected financial criteria but here’s the key: we never compare a stock to the wrong peer group. Each stock is only evaluated relative to the industry average within its own market cap category.
To make industry comparisons fair and statistically sound, we calculate the mean and standard deviation for each metric within the same industry and market cap group, **excluding outliers**. Outliers are identified using the interquartile range (IQR) method, and removed before calculating averages and z-scores. 

#### Preliminary criteria: 
To be considered “undervalued,” a stock must meet all of these:
- P/FCF > 0 and below the industry average
- P/B > 0 and below the industry average
- A/E > 1 and below the industry average
- ROE > 10%
- ROA > 5%

#### Additional criteria: 
We further rank stocks based on these bonus signals:
- P/B < 70% of industry average
- ROE > industry average
- ROA > industry average
- P/E < industry average
- P/E between 1 and 25

For each criterion met, a stock gets 1 point. The highest score a stock can get is 5 points.

## Dashboards that Tell a Story

### Dashboard 1: Undervalued Stocks

I created this interactive dashboard to help users explore the top-scoring undervalued stocks across sectors based on the criteria in our framework.

<iframe title="Undervalued Stocks Dashboard" width="1280" height="780" src="https://app.powerbi.com/view?r=eyJrIjoiNzUyMmMxOTctMzM4Mi00YTRjLTkyNjEtNDVlNzBlZWE0NzhjIiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9&pageName=6e69fbbbad14ed7e6c39" frameborder="0" allowFullScreen="true"></iframe>

#### Key Features & How to Use Them

This dashboard showcases stocks that meet preliminary undervaluation criteria, then scores and ranks them to help users identify top opportunities.

**1. Filter by Sector and Market Cap:** You can use the filters at the right corner to select a sector (e.g., Communication Services) and market cap (Large, Mid, or Small). This tailors the view to peer groups for fair comparison.

**2. Score-Based Stock Evaluation:** All stocks shown have already passed the baseline filters. Each stock is then evaluated on five additional criteria. It earns 1 point for each one met, with a maximum score of 5. The score for each stock (0-5)is shown as a horizontal stacked bar with one color-coded block per point.

**3. Z-Score Matrix:** Shows how far a stock’s metric deviates from the industry average. This helps users compare each stock to its peers.

Undervalued metrics:
- P/FCF, P/B, A/E, P/E → negative z-score is better  
- ROE, ROA → positive z-score is better

Z-scores that go in the “wrong” direction (e.g. high P/E) are grayed out.
Z-scores further from 0 (stronger deviations) are shaded in darker green, making standout values easy to spot.

**4. Summary Cards:** In the dashboard, you’ll find 6 cards showing the top 3 stocks for each fundamental metric (based on z-score). These cards help users quickly identify leaders in: P/FCF, P/B, ROE, ROA, A/E, P/E

**5. Metric Breakdown Table:** Scrollable table with detailed financial metrics for each stock.

**6. Tooltips for Context:** Hover over the visuals to get deeper insight. Tooltips show a stock's industry, market cap, current price and score for additional criteria.

### Dashboard 2: Industry Averages

I also created a dashboard showing industry averages of individual metrics to help users understand the financial “norms” for each industry and market cap group.

<iframe title="Industry Averages Dashboard" width="1280" height="780" src="https://app.powerbi.com/view?r=eyJrIjoiZjBkYTRjNjUtYzQ2Yy00ZTNmLWFkNzMtY2Y0ZGVlMjdjNTQ0IiwidCI6IjEwZGVlN2UzLWJjMGQtNGNjNy1iMzZhLWEzZDQzMGEzZGI5ZCIsImMiOjZ9" frameborder="0" allowFullScreen="true"></iframe>

#### Key Features & How to Use Them

This dashboard provides a high-level view of how financial fundamentals vary across sectors and industries. You can use the slicers to narrow the view to the industry and market cap in you're interested in.

Each visual displays industry-level averages for six core financial metrics, broken down by sector and market cap group (Large, Mid, Small):
- Average P/FCF
- Average P/B
- Average ROE
- Average ROA
- Average A/E
- Average P/E

These averages are calculated after filtering out outliers using the interquartile range method. 

Users can use this dashboard to identify which industries are overhyped with lower profitability (ROE, ROA) but higher valuations (P/B, P/E, P/FCF).


## Automating the Mess: Turning Chaos into Clean Data

Initially, my husband manually cleaned and analyzed the raw stock data in Excel. But with 11 sector-specific datasets and dozens of formulas, the process quickly became time-consuming, repetitive, and prone to error, especially with frequent data updates. Each refresh could take hours.

I completely re-engineered the process to be fast, accurate, and user-friendly by implementing a set of tools:
- Power Query (20+ custom functions): For automatic cleaning, transformation, and metric calculation across all datasets.
- VBA Macros: To refresh all data and recalculate results with a single click.
- Dynamic file paths: So the project works across any machine without broken links.
- Pivot tables: To calculate industry averages while filtering outliers.
- RTD function for real-time stock prices: the RTD (Real-Time Data) function integrates with the Thinkorswim platform to pull real-time stock prices directly into the workbooks.
- Conditional formatting: To surface strong candidates visually, making stock analysis easier for non-technical users.

After processing the data in Excel, I brought the results into Power BI, where I created interactive dashboards that:
- Compare metrics across sectors and industries
- Highlight top-ranking undervalued stocks
- Visualize trends in P/E, ROE, ROA, and other key indicators
- Enable non-technical users to explore insights without needing to touch the raw data

All DAX measures were designed to align with the logic used in Excel, ensuring consistency between platforms.

## Final Thoughts

This project started with a shared curiosity and turned into a complete, repeatable workflow that saves hours and delivers clear insights. It was as much about collaboration as it was about technology. Working closely with my husband, a non-technical stakeholder, I used an informal agile approach by delivering in small chunks, gathering feedback, and adapting quickly. Clear communication and step-by-step guides I created helped my husband transition smoothly to the new process. I’m proud to have taken initiative, self-taught new skills ahead of coursework, and built a fully automated system that saves time and drives smarter investment decisions.

The real win? Building something that works for both analysts and non-technical users alike. It reminded me that the best data projects don’t just analyze — they simplify. They turn mess into clarity and help people make better, faster decisions.

That’s what I aim to build, every time.
