---
layout: post
title:      "Data Scraping Time"
date:       2021-05-19 07:09:58 +0000
permalink:  data_scraping_time
---


It may be intuitive that high complexity models may required long amount of time. However, data scraping from the web, and also reading the web data and getting it into a usable format may also take very long. Here are some of my experiences:

* Scraping EDGAR for S&P500 10-Q quarterly statement for 10 years, first pass -> 1 hr 9 mins
* Second pass to get missing items from URL failtures -> 15 min each
* SP500 daily stock history for 10 years using yfinance -> couple mins
* Extracting pandas dataframe (using pd.read_html) for EGDGAR htmls (~6000 htmls to ~11000 html) -> 17 hr to 1 day and 10 hr 

These also take a looooong time. Remember to budget data scraping and extraction when budgeting time of work!
