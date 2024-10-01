---
title: "UtahStats Dating Survey Report"
description: I partnered with the Instagram account UtahStats to learn about dating culture in Provo/Orem. Here I share what I learned from the data regarding young adult lifestyle, college, dating, relationships, and other interesting topics, and how the analysis turned into my first ever marketable product.  
layout: post

github:
    is_project_page: true
    repository_name: UtahStats
    repository_url: https://github.com/jxnpass/UtahStats

date: 2024-9-29 17:50:00
---

STILL IN DEV

## Table of Contents
- [Introduction](#Introduction)
- [Synopsis](#Synopsis)
- [Conclusion](#conclusion)

## Introduction
Last year, I deleted Instagram completely. I was wanting to make a change from my lifestyle where I wasted hours and hours on reels each day. Later in November, however, my family urged me to redownload it and start a fresh profile, looking for more meaningful accounts to follow. That was when I stumbled upon the Instagram profile [@UtahStats](https://www.instagram.com/utahstats/). With my love of data analytics in the realm of human behavior, psychology, and culture, this profile became a major source of excitement. I would tell my friends to follow this account purely because of how interesting their insights were, and where I think my stats background could help improve the reporting. As I approached the summer of 2024 and an enrollment in a Statistcs masters program at BYU, I wanted to explore more statistical psychology. I reached out to the account owner, Jacob Dunn, purely on a whim, asking if he had a project he would want to collaborate on, or at least have me contribute to. After a couple of discussions, we landed on an idea for a data analytics project with an unpredictable outcome: a summary of his first ever survey.   

As a psychology student at BYU, Jacob Dunn had a desire to explore niche facts about college students living in Utah. He learned how statistics can be utilized to study various populations. He created the first "ProvoStats" survey (as it was named then) to collect data, originally passing out fliers to invite students to take the survey and contribute their experiences. Once enough data was collected, Jacob posted unique findings on Instagram. Overtime, the page grew tremendously. As he kept posting more of his findings, Instagram followers demanded more answers to questions about young adult culture. This led to Jacob further enrichening his range of topics by creating multiple surveys with more specialized questions. This opened opportunities for followers from outside Utah County to respond to surveys and contribute to the data, hence creating the brand [@UtahStats](https://www.instagram.com/utahstats/).

Participants of the @UtahStats surveys are presented with a broad range of questions, and their responses are recorded and processed using Qualtrics. These questions range from topics such as previous relationships, dating, church and college activity, politics, and other topics unique to the Utah County area.  

## Synopsis

With a sample of 2,101 respondents (and 1,881 had usable data). From our quick exploration of the data and the **table 1** below, we understood some of the main characterstics of our sample:
- While the range of our sample covers ages between 18 and 30, **75% are below 23 years of age.**
- 75% of survey respondents attend BYU and 14% attend UVU. **This emphasizes a geographical response bias towards BYU/Provo young adults being more regular participants than Orem/UVU.** 
- 96% of survey respondents are of the LDS faith.
- 57% of survey respondents served missions (and 54% of missionaries served in foreign missions).

![table1](/assets/UtahStats/table1.png)

The next couple sections discuss some of my personal favorites from the paper as they both present some very intersting findings and gave me the opportunity to tap into statistical and technical skills.

### Ineference on Monthly Dates and Car Ownership
![f4.7](/assets/UtahStats/figure4.7.png)

### Monte Carlo Simulation on Female’s Minimum Height for Male Partner 
![f7.3](/assets/UtahStats/figure7.3.png)

```
# Monte Carlo Simulation: potential height differences and preferences between males and females # 
n <- 50000 # number of couples to make

sample_female <- female_data[sample(x = 1:nrow(female_data), size = n, replace = T),]
sample_male <- sample(x = male_data$height, size = n, replace = T)
height_differences <- sample_male - sample_female$height
height_requirements <- sample_male - sample_female$height_requirement

# Monte Carlo Insights #
mean(height_differences < 0)
sd(sample_diffs < 0) / sqrt(n)
# 7% of women may find a randomly assigned male partner at least an inch shorter than her
# MC Error: 0.1%

mean(sample_reqs < 0)
sd(sample_reqs < 0) / sqrt(n)
# 20% of women will not find a randomly assigned man that meets their height requirements 
# MC Error: 0.2%
```

![f7.4](/assets/UtahStats/figure7.4.png)

## Conclusion

I learned a lot about how to report statistical inference with a lot of complications in statistical reasoning in mind, namely survey response biases, imbalanced groups, and reporting findings under the pretense of a generally non-academic audience and doing so **with statistical cautions** in place. I also experienced how to tell a compelling story using visualizations and tables, and explaining to readers what data visualizations can teach them about Utah culture. 

