---
layout: post
title: "U.S. YouTube Video Trends: A Tableau Dashboard Story"
description: >
  An interactive Tableau dashboard that visualizes U.S. YouTube trending data to reveal viewer sentiment, top channels, and regional content preferences.
image: /assets/img/posts/3/eyestetix-studio-Bm-5o5M2mAI-unsplash.jpg
tags: [youtube, tableau dashboard, data visualization]
---

In this Tableau project, I explored trending YouTube videos across the U.S. to uncover insights into viewer sentiment, content performance, and regional preferences.

<a href="https://github.com/nvu01/Tableau-Public-Dashboard/tree/main" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo
</a>

👉 [View the dashboard here](https://public.tableau.com/app/profile/ngan.vu3144/viz/U_S_YouTubeVideoTrends/U_S_YouTubeVideoTrends)


* toc
{:toc .large-only}


## What I Built — And Why It Matters

Using a cleaned dataset from Kaggle, I explored trending YouTube video statistics. I designed four interactive visualizations to tell a story and answer deeper questions that go beyond surface metrics like views or likes:

- Do more popular videos also attract more criticism?
- Which creators consistently break through the noise?
- Are some categories winning because of volume, or higher per-video impact?
- How does content preference vary across the U.S.?

This analysis is powered by four main visualizations:

1. **Likes vs. Dislikes Across YouTube Categories (Scatter Chart)**: 
This chart explores the relationship between the number of likes and dislikes for videos within different categories. It offers insights into viewer sentiment and how engagement varies by content type.

2. **Top 20 YouTube Channels (Bar Chart)**: 
A bar chart that ranks the top 20 YouTube channels by total views. This visualization highlights the most influential content creators and provides a comparison of their reach and audience engagement.

3. **Video and View Counts by Category (Dual-Axis Bar Chart)**: 
This dual-axis chart compares the number of videos and total view counts across various YouTube categories. It helps to identify which categories are most popular in terms of content volume and viewer engagement.

4. **Top YouTube Categories by State (Interactive Map)**: 
An interactive map showing the most popular YouTube categories in each U.S. state. This visualization offers a regional perspective on video trends and helps understand geographic differences in content preferences.

## Interactive Dashboard

Explore the full dashboard here, filter by category or hover over charts to get deeper insights.

{% raw %}
<iframe 
  src="https://public.tableau.com/views/U_S_YouTubeVideoTrends/U_S_YouTubeVideoTrends?:showVizHome=no&:embed=true" 
  width="1280" 
  height="720px" 
  frameborder="0" 
  allowfullscreen>
</iframe>
{% endraw %}

## Guided Story: A Walkthrough of Insights

This Tableau Story walks you through the key findings, one insight at a time.

{% raw %}
<iframe 
  src="https://public.tableau.com/views/StoryU_S_YouTubeVideoTrends/Story?:showVizHome=no&:embed=true" 
  width="1000" 
  height="800px" 
  frameborder="0" 
  allowfullscreen>
</iframe>
{% endraw %}

