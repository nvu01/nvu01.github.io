---
layout: post
title: "U.S. YouTube Video Trends: A Tableau Dashboard & Story"
description: >
  An interactive Tableau dashboard that visualizes U.S. YouTube trending data to reveal viewer sentiment, top channels, and regional content preferences.
image: /assets/img/posts/3/eyestetix-studio-Bm-5o5M2mAI-unsplash.jpg
tags: [youtube, tableau dashboard, data visualization]
---

In this Tableau project, I explored trending YouTube videos across the U.S. to uncover insights into viewer sentiment, content performance, and regional preferences.

<a href="https://github.com/nvu01/Tableau-Public-Dashboard/tree/main" target="_blank" rel="noopener">
  <i class="icon-github"></i> GitHub Repo
</a>

* toc
{:toc .large-only}

## Datasets Overview

For my data visualization project, I am using datasets containing statistics on trending YouTube videos in the U.S. These datasets were originally sourced from Kaggle and then transformed and cleaned by Udacity for educational purposes. The cleaned datasets can be found in my GitHub repo.

Data source: [Kaggle](https://www.kaggle.com/datasets/datasnaek/youtube-new/data?select=USvideos.csv)


## What I Built and Why

I designed four interactive visualizations to tell a story and answer deeper questions that go beyond surface metrics like views or likes:

- Do more popular videos also attract more criticism?
- Which creators consistently break through the noise?
- Are some categories winning because of volume, or higher per-video impact?
- How does content preference vary across the U.S.?

### Key Visualizations:

The analysis is powered by four main visualizations:

**1. Top 20 YouTube Channels (Bar Chart)**:

To identify the most influential creators, I built a bar chart ranking the top 20 YouTube channels by total views. Since trending videos in the dataset appear repeatedly across multiple dates (as long as it remained trending), I used Tableau's Level of Detail (LOD) calculation to ensure only the maximum view count per unique video was used in the plot, avoiding duplicate entries. Then I aggregated these values to get the total views per channel.

**2. Likes vs. Dislikes Across YouTube Categories (Scatter Plot)**: 

The scatter plot reveals the relationship between likes and dislikes for trending videos in different categories. Each data point represents an individual video. The shape of each point corresponds to the video’s category, so users can immediately identify content types without relying on color alone. 

I added a "Category Name" filter to let users focus on specific genres (like Comedy or Music) and investigate how sentiment patterns vary.

**3. Video and View Counts by Category (Dual-Axis Bar Chart)**: 

This chart addresses an important question: is volume or impact more important in content trends?

I created a dual-axis chart to show:
- Bar chart: Total view counts per category (aggregated from highest view count per video)
- Dot plot: Number of unique trending videos in that category

I also structured the hierarchy with Channel Title nested under Category Name, so users can drill down into specific creators within each genre.

**4. Top YouTube Categories by State (Interactive Map)**: 

The interactive map shows regional preferences with each state colored by its most popular YouTube category (based on total views). This visualization offers a regional perspective on video trends and helps understand geographic differences in content preferences.

Users can also apply the Category Name filter to see where specific content types are trending, even if they’re not the most dominant in that state. This interaction makes it easy to investigate niche audiences or regional differences in taste.

### Tooltips

Every chart in the dashboard includes tooltips that appear when users hover over data points. These tooltips provide additional context such as video titles, channel names, categories, view counts, likes, and dislikes, without cluttering the visual space. This design choice keeps the interface clean while giving users quick access to details for deeper insight.


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


## Key Takeaways

- **Popularity attracts polarity.** Trending videos with high likes often come with a high number of dislikes.
- **Big brands dominate.** Marvel Entertainment and YouTube Spotlight top the charts in total views.
- **Music wins in impact.** Fewer videos, but each with massive reach.
- **Geography matters.** Music reigns nationwide, but Entertainment and Gaming see regional spikes.


## Final Thoughts

With Tableau, I turned a complex dataset into an accessible, interactive tool that surfaces insights through design and exploration. But this project was more than just building a dashboard. It was an exercise in turning raw data into narrative. Beyond the technical skills, this project pushed me to think like a storyteller, to guide users through the data, not just analyze it.