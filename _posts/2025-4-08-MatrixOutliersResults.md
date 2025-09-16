---
title: "Outlier Detection Algorithm -- Part 4: Simulation Results for Detecting Cellwise Outliers"
description: This post illustrates how detectable cellwise outliers are in various settings within a Monte Carlo simulation framework (discussed in Part 3). This post also provides the baseline for comparing Marginalized Mahalanobis (MaMa) to its competitors.
layout: post

github:
    is_project_page: false
    repository_name: 
    repository_url: 

tags: [Data Science, R, Outlier Detection, Simulations]
date: 2025-4-08 7:50:00
---

## Table of Contents
- [Introduction](#introduction)
- [Results](#results)
- [Conclusion](#conclusion)
- [Awards](#awards)

## Introduction

This post presents a comprehensive simulation study designed to evaluate outlier detection algorithms under a wide variety of challenging conditions. Specifically, I investigate how well MaMa and competing algorithms perform across different cellwise outlier types (A, B, and C, introduced in [Part 2](/_posts/2025-2-21-MatrixOutlierTypes.md)), across different underlying data distributions (MVN, log-MVN, and bimodal MVN, discussed in [Part 3](/_posts/2025-3-26-MatrixOutlierAlgorithms.md)), and across different covariance structures (“A09”, “ALYZ”, and “Rho”).

To stress-test these algorithms and compare them to MaMa, I simulate datasets with increasing levels of outlier effect size and outlier rate, then assess each algorithm's accuracy, precision, recall, and F1 score. This study provides a visual and intuitive way to compare algorithm performance across a massive design space—ideal for anyone designing or choosing an outlier detection method for multi-dimensional data.

## Results

For our simulation, we are particularly interested in seeing how MaMa performs against its competitors. Each algorithm's performance is visualized through line plots, tracking how metrics such as **accuracy**, **precision**, **recall**, and **F1 score** change under varying conditions. The results are organized into subsections based on outlier type, data distribution, and covariance structure, with two main scenarios analyzed:

Increasing Effect Size:

- The proportion of outliers is fixed at 5% per column (no duplicate cells).

- This scenario tests how well algorithms respond to weaker and stronger outliers.

Increasing Outlier Rate:

- The effect size is held constant (set to 3 for Types A and C, and to min/max for Type B).

- This scenario evaluates how performance degrades or improves as more outliers are introduced.

Each chart within the subsections illustrates how each algorithm’s performance evolves, helping identify which methods are more robust across different kinds of contamination and data structures.

### Type A Outliers

Type A outliers are simply created by altering $X_{ij}$ to be  $X_{ij} \pm z*SD(X)$. A higher effect size $z$ creates a more conspicuous outlier.

**MVN**

It's important to recall that all five algorithms we explore here (cellGMM, cellMCD, DDC, DI, and MaMa), were built to detect cellwise outliers under a standard multivariate normal distribution. Under the effect size figure, we see each algorithm perform exceptionally well. However, some algorithms struggle to handle high contamination. As the contamination of cellwise outliers grow, some of models like cellGMM and DDC tend to struggle greatly. These algorithms do not have explicit hyperparameters that make initial predictions on the rate of contamination.

<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type A/MVN-A09-OutA.png" alt="MVN-A09-OutA-Effect" style="width: 100%;">
    <figcaption>Each algorithm performs well under a strongly intercorrelated (A09) dataset</figcaption>
  </figure>
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type A/MVN-A09-OutA.png" alt="MVN-A09-OutA-Rate" style="width: 100%;">
    <figcaption>However, certain algorithms struggle under higher contamination rates</figcaption>
  </figure>
</div>

**Bimodal MVN**

Let's consider the scenario where we combine two MVN clusters into a dataset. For this case, we see that MaMa and cellGMM do the best under various effect sizes and most outlier rates. Cell GMM was trained to identify outliers under "heterogenous data", and thus are built to excel in this type of data. However, higher percentages of outliers are a struggle for this algorithm. MaMa seems to handle each of these cases exceptionally well compared to competitors.   

<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type A/bi_MVN-ALYZ-OutA.png" alt="bi_MVN-ALYZ-OutA-Effect" style="width: 100%;">
    <figcaption>MaMa and cellGMM are optimal algorithms under bimodal MVN </figcaption>
  </figure>
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type A/bi_MVN-ALYZ-OutA.png" alt="bi_MVN-ALYZ-OutA-Rate" style="width: 100%;">
    <figcaption>cellGMM loses reliability at higher percentages of cellwise outliers </figcaption>
  </figure>
</div>

**Log MVN**

When expanded to a logarithm MVN, MaMa makes promising strides. While detecting outliers gets trickier under this scenario, MaMa is able to pick up on the outlier trend faster than its competitors as the effect size grows. However, predictive accuracy dips downward unforunately under higher rates of outliers. Why is this the case? There is an important concept to establish here: the rate graphic is not to illustrate how MaMa performs worse under higher outlier percentages, but how cellMCD, DDC, and DI fail to establish any connection under **ALL** outlier rates. Note how precision is stuck at 100% for these three algorithms. Because each algorithm is trained to predict cellwise outliers far from its data center, it fails to determine if the naturally skewed observations found in a log MVN distribution are inliers, which inevitably creates over-sensitive classifications. Thus, the recall is so high, and the precision is so low for lower rates. However, as outlier percentage grows in the study, the trend for precision and F1 increases, making it a more attractive choice on paper, but ultimately not optimal for this type of algorithm. Thus, even though MaMa declines in performance with higher rates, it is very much preferred over these competing algorithms. 

<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type A/log_MVN-Rho-OutA.png" alt="log_MVN-Rho-OutA-Effect" style="width: 100%;">
    <figcaption>MaMa is the obvious choice when detecting outliers in this distribution</figcaption>
  </figure>
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type A/log_MVN-Rho-OutA.png" alt="log_MVN-Rho-OutA-Rate" style="width: 100%;">
    <figcaption>MVN-trained cellwise algorithms like DDC improve under the 'false' advantage of high outlier rates  </figcaption>
  </figure>
</div>

### Type B Outliers

Type B outliers require much more scrutiny in cleaning. This is because Type B outliers require consideration of the correlation structure of the dataset, as each value, including the cellwise outliers, are within the range of each variable. A Type B outlier is created when a cell value is pulled outside of the correlation structure such that it surpasses the quantile of Mahalanobis distances (MD) found within the true data (more explanation in [Part 2](/_posts/2025-2-21-MatrixOutlierTypes.md)). This quantile effect increases from the 90th to the 100th (maximum) to test different predictive outcomes.  

For these examples, I decided to use the "A09" covariance matrix as it creates datasets with the greatest amount of multicollinearity, allowing outliers to stand out more and algorithms to be more comparable. 

**MVN**

Under the MVN Type B outliers, we see that MaMa is comparatively underperforming in precision, but doing mediocre in F1 and recall. Interestingly, MaMa performs well under various outlier percentages. While it is less accurate at detecting outliers at the lower rates, it keeps the same consistency under higher rates. 

<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type B/MVN-A09-OutB.png" alt="MVN-A09-OutB-Effect" style="width: 100%;">
    <figcaption>MaMa underperforms under Type B in the MVN case </figcaption>
  </figure>
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type B/MVN-A09-OutB.png" alt="MVN-A09-OutB-Rate" style="width: 100%;">
    <figcaption>Unlike other algorithms, MaMa stays consistent under changing outlier rates </figcaption>
  </figure>
</div>

**Bimodal MVN**

MaMa and Cell GMM perform exceptional in the bimodal case and are almost equally optimal for various MD quantiles. However, cellGMM has a poor recall, so it makes very "safe" classifications for cellwise outliers. Additionally, and similar to the MVN case, MaMa reveals greater consistency under various outlier percentages, again unlike cellGMM. 

<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type B/bi_MVN-A09-OutB.png" alt="bi_MVN-A09-OutB-Effect" style="width: 100%;">
    <figcaption>MaMa and cellGMM perform well under Type B in the bimodal MVN case </figcaption>
  </figure>
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type B/bi_MVN-A09-OutB.png" alt="bi_MVN-A09-OutB-Rate" style="width: 100%;">
    <figcaption>MaMa keeps consistency under changing outlier rates unlike cellGMM </figcaption>
  </figure>
</div>

**Log MVN**

The line chart figures below suggest interesting trends for MaMa. For the quantile increases, MaMa struggles at first, but sharply outperforms the other methods in classifying outliers. For the other four models, there is a certain percentile (around 92.5th to 95th) where we witness no improvement in classification. For the outlier rates, MaMa is clearly performing best in detection up until around 20%, where it takes a sharp decline. The logic behind this trend is unknown as of now, but future research may consider why MaMa had struggled in this area so uniquely. 

<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type B/log_MVN-A09-OutB.png" alt="log_MVN-A09-OutB-Effect" style="width: 100%;">
    <figcaption>MaMa stands out as an optimal model for classifying outliers under higher quantiles </figcaption>
  </figure>
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type B/log_MVN-A09-OutB.png" alt="log_MVN-A09-OutB-Rate" style="width: 100%;">
    <figcaption>MaMa outperforms all models up until around 20%, where it declines sharply </figcaption>
  </figure>
</div>

### Type C Outliers

Type C is the simplest case of outliers, where a random percentage of cells within a column are replaced with a set value. This style of outlier creation was designed by Raymaekers and Rousseeuw and the `generateData` function in the `cellWise` package. To maintain the designed integrity of this outlier, we only consider the MVN and the bimodal MVN cases, as this function was designed to generate MVN data. 

**MVN**

For the MVN case, it appears that MaMa and cellGMM perform the best under Type C outliers with changing effects. There also appears to be some effect size where DDC, cellMCD, and DI cannot improve further. For growing outlier rates, MaMa again performs the most consistently. 

<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type C/MVN-ALYZ-OutC.png" alt="MVN-ALYZ-OutC-Effect" style="width: 100%;">
    <figcaption>MaMa and cellGMM are the top performers under MVN Type C  </figcaption>
  </figure>
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type C/MVN-ALYZ-OutC.png" alt="MVN-ALYZ-OutC-Rate" style="width: 100%;">
    <figcaption>MaMa performs the most consisently under all outlier percentages </figcaption>
  </figure>
</div>

**Bimodal MVN**

The line charts for this case had very unique trends. We see under growing effect size that each method seems to improve its classification, almost at the same rate. With outlier percentages, however, we see that each method does not perform well at all.

<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type C/bi_MVN-Rho-OutC.png" alt="bi_MVN-Rho-OutC-Effect" style="width: 100%;">
    <figcaption>All methods improve in performance when effect size grows </figcaption>
  </figure>
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type C/bi_MVN-Rho-OutC.png" alt="bi_MVN-Rho-OutC-Rate" style="width: 100%;">
    <figcaption>Each method reveals poor performance in one or more metrics </figcaption>
  </figure>
</div>

## Conclusion

The following post presents that MaMa, while perhaps not the best method across all types of situations, proves very versatile in many of them. This is a critical aspect for those having no prior knowledge about their data, wishing to review potential outliers or typos in the data, and wanting the most efficient way to find them. 

This is the first of many simulations that I perform. To see the next simulation style, I recommend reading [part 5!]()


## Awards

BYU held their 2025 Student Research Conference where I could to present my research to! I am estatic to share that I was the selected [winner of my session](https://src.byu.edu/winners/2025) (against 6 other student presenters) from the research I describe here. 

<div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
  <figure style="width: 90%; text-align: center;">
    <img src="/assets/MO4/SRCWinners.JPG" alt="SRCWinners" style="width: 100%;">
  </figure>
</div>

