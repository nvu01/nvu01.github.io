---
layout: post
title: "Undervalued Stock Scanner: From Raw Data to Smart Insights"
description: >
  Add short description here.
image: /assets/img/posts/2/adam-smigielski-K5mPtONmpHM-unsplash.jpg
tags: [dashboard, stock market, financial market]
---

Like many aspiring investors, my husband and I were drawn to the challenge of identifying undervalued stocks because they are like hidden gems with solid fundamentals that the market hasn't caught up with yet. What started as a weekend project in Excel became a fully automated pipeline combining Power Query, VBA, and Power BI dashboards. 



<a href="https://github.com/nvu01/Undervalued-Stock-Scanner" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo
</a>

**Disclaimer: This project is intended for educational and informational purposes only. The analysis, models, and methodologies used in this project are not intended to serve as financial or investment advice. The information presented should not be construed as a recommendation to buy, sell, or hold any securities or assets. Investing in the stock market carries inherent risks, and any decisions based on the content of this project are solely the responsibility of the individual. Always consult with a qualified financial advisor before making any investment decisions.**

* toc
{:toc .large-only}

## 🎯 Project at a Glance

This project started over casual investment conversations with my husband. While my husband handled the financial theory, I built a repeatable, error-resistant data solution. Our goal? Identifying potentially undervalued stocks by analyzing key financial metrics across various sectors. The project focuses on three market cap categories (Large Cap, Mid Cap, and Small Cap) and applies statistical methods to assess stock fundamentals.

It taught me the importance of scalable workflows, modular data cleaning, and clear visual storytelling skills I now use professionally in analytics.
The Undervalued Stock Scanner project aims to help 

## 📂 Datasets

We worked with 11 raw CSV files exported from Thinkorswim. Each file representing a different sector. These datasets contain stock fundamentals, segmented by market cap:

- Large-Cap: $10B+
- Mid-Cap: $2B–$10B
- Small-Cap: $250M–$2B

Each sector includes multiple industries. When comparing stocks, it's important to consider market capitalization and industry because a “good” metric in one industry or market cap can be a red flag in another. We structured the pipeline to retain this nuance throughout the analysis.

## 🧠 What Makes a Stock Undervalued?

### Key Fundamentals

Here's a quick breakdown of the core financial indicators used in our evaluation and why they matter:

#### Price-to-Free Cash Flow ratio (P/FCF)
Price-to-Free Cash Flow (P/FCF): A high P/FCF ratio indicates that the specific firm is trading at a high price but is not generating enough free cash flows to support the multiple (sometimes this is OK, depending on the firm, industry, and its specific operations). Smaller price ratios are generally preferred, as they may reveal a firm generating ample cash flows that are not yet properly considered in the current share price.
#### Price-to-Book ratio (P/B)
Book Value Per Share indicates a firm's net asset value minus total liabilities per share. When a stock is undervalued, it will have a higher BVPS than its stock price in the market.
Price-to-book value (P/B) ratio measures the market's valuation of a company relative to its book value. Thus, P/B=1 means it is traded at exactly where it should be. Higher P/B means it might be overvalued.
#### Return on Equity (ROE)
This ratio is a gauge of a corporation's profitability and how efficiently it generates those profits. The higher the ROE, the better a company is at converting its equity financing into profits.
#### Return on Assets (ROA)
Return on assets is a profitability ratio that shows how much profit a company generates from its assets. Return on assets (ROA) measures how effective a company's management is in generating profit from the total assets on its balance sheet. A ROA that rises over time indicates that the company is doing well at increasing its profits with each investment dollar it spends.
#### Asset-to-equity ratio (A/E)
The asset-to-equity ratio measures a company's financial leverage by comparing its total assets to its shareholders' equity. A higher ratio indicates the company is using more debt to finance its assets, suggesting a higher financial risk. A lower ratio suggests a more conservative capital structure with less reliance on debt. 
#### Price-to-Earnings ratio (P/E)
The price-to-earnings ratio is a valuation metric used to assess a company's stock price in relation to its earnings per share. It essentially shows how much investors are willing to pay for each dollar of a company's earnings. A high P/E ratio could mean that a company's stock is overvalued or that investors expect high growth rates. A low P/E can indicate that a company is undervalued or that a firm is doing exceptionally well relative to its past performance.

### How We Evaluate Stocks Using These Metrics
Our evaluation is based on a series of carefully selected financial criteria but here’s the key: we never compare a stock to the wrong peer group. Each stock is only evaluated relative to the industry average within its own market cap category.
To make industry comparisons fair and statistically sound, we calculate the mean and standard deviation for each metric within the same industry and market cap group, **excluding outliers**. Outliers are identified using the interquartile range (IQR) method, and removed before calculating averages and z-scores. This ensures extreme values don’t distort our benchmarks, giving a more accurate picture of how a stock performs relative to its peers.
#### Preliminary criteria: 
To be considered “undervalued,” a stock must meet all of these:
- Positive Price-to-Free Cash Flow ratio: P/FCF > 0
- Positive Price-to-Book ratio: P/B > 0
- These ratios should be below the industry's average within a market cap: P/FCF, P/B, A/E
- Return on Equity ratio is greater than 10%: ROE > 10
- Return on Assets ratio is greater than 5%: ROA > 10
- Asset-to-equity ratio is greater than 1: A/E > 1

#### Additional criteria: 
We further rank stocks based on these bonus signals:
- P/B < (0.7 * Mean P/B within industry group)
- ROE and ROA should outperform the industry
- Price-to-Earnings ratio should be below the industry's average within a market cap and between 1 and 25

For each criterion met, a stock gets 1 point. The highest score a stock can get is 5 points.

## 📊 Dashboards that Tell a Story

### Dashboard 1: Undervalued Stocks
Purpose:
To highlight the top-scoring undervalued stocks across sectors — based on the criteria in our conceptual framework.

Key Visuals:

Example Insight:


### Dashboard 2: Industry Averages

Purpose:
To help users understand the financial “norms” for each industry and market cap group — so undervalued stocks can be spotted in context.

Key Visuals:

Example Insight:

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


