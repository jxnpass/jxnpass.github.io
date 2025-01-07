---
title: Wikipedia Scraper on Streamlit
description: Wikipedia data is boundless, insightful, and difficult to access for personal use. I developed a Streamlit app that utilizes Python's webscrapping features to read and write data files straight from Wikipedia tables. 
layout: post

github:
    is_project_page: true
    repository_name: WikipediaTableScraper
    repository_url: https://github.com/jxnpass/WikipediaTableScraper

tags: [Python, Web-Scraping, Dashboards]
date: 2025-1-4 17:50:00
---

In today's data-driven world, there is a growing need for accessible and user-friendly tools that can quickly harness insightful information from publicly available resources like Wikipedia. One such tool I present is this web scraping interface that allows users to extract tables from Wikipedia pages, clean the data, and transform it into a usable format. By leveraging Python's BeautifulSoup package, this app makes it simple to identify and scrape tables, rows, and columns, while also distinguishing between numeric and non-numeric data. This capability helps users easily access and analyze data from Wikipedia without the need for manual copying and pasting, streamlining the process significantly.

The app, built using Streamlit, enhances user interactivity by enabling the editing of specific cells within the scraped data. Users can modify the content of the table directly within the app, ensuring it meets their needs. Once the data is cleaned, the tool allows users to download the processed table in a CSV or Excel format, making it easy to share or further analyze. As the next step in this project, integrating Plotly will enable the creation of visual graphics, offering dynamic plots and charts that bring the data to life. By extending the functionality to visualize the extracted data, this tool will provide a comprehensive data manipulation and visualization pipeline for users, allowing for deeper insights and better decision-making.

<iframe
  src="https://wikiscraper.streamlit.app?embed=true"
  style="height: 600px; width: 100%;"
></iframe>

The app above is usable for testing and for personal needs. You can also [view the app directly](https://wikiscraper.streamlit.app/) through Streamlit Cloud. The three links on the dashboard work well, but there may be notable shortcomings found when using other Wikipedia URLs. 
