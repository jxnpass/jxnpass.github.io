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
- [Discussion](#discussion)
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

**MVN**
It's important to recall that all five algorithms we explore here (cellGMM, cellMCD, DDC, DI, and MaMa), were built to detect cellwise outliers under a standard multivariate normal distribution. Under the effect size figure, we see each algorithm perform exceptionally well. However, some algorithms struggle to handle high contamination. As the contamination of cellwise outliers grow, some of models like cellGMM and DDC tend to struggle greatly. These algorithms do not have explicit hyperparameters that make initial predictions on the rate of contamination.

<div style="display: flex; justify-content: center; gap: 10px;">
  <figure style="width: 65%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type A/MVN-A09-OutA.png" alt="MVN-A09-OutA-Effect" style="width: 100%;">
    <figcaption>Each algorithm performs well under a strongly intercorrelated (A09) dataset</figcaption>
  </figure>
  <figure style="width: 65%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type A/MVN-A09-OutA.png" alt="MVN-A09-OutA-Rate" style="width: 100%;">
    <figcaption>However, certain algorithms struggle under higher contamination rates</figcaption>
  </figure>
</div>

**Bimodal MVN**
Let's consider the scenario where we combine two MVN clusters into a dataset. For this case, we see that MaMa and cellGMM do the best under various effect sizes and most outlier rates. Cell GMM was trained to identify outliers under "heterogenous data", and thus are built to excel in this type of data. However, higher percentages of outliers are a struggle for this algorithm. MaMa seems to handle each of these cases exceptionally well compared to competitors.   

<div style="display: flex; justify-content: center; gap: 10px;">
  <figure style="width: 65%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type A/bi_MVN-ALYZ-OutA.png" alt="bi_MVN-ALYZ-OutA-Effect" style="width: 100%;">
    <figcaption>MaMa and cellGMM are optimal algorithms under bimodal MVN </figcaption>
  </figure>
  <figure style="width: 65%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type A/bi_MVN-ALYZ-OutA.png" alt="bi_MVN-ALYZ-OutA-Rate" style="width: 100%;">
    <figcaption>cellGMM loses reliability at higher percentages of cellwise outliers </figcaption>
  </figure>
</div>

**Log MVN**
When expanded to a logarithm MVN, MaMa makes promising strides. While detecting outliers gets trickier under this scenario, MaMa is able to pick up on the outlier trend faster than its competitors as the effect size grows. However, predictive accuracy dips downward unforunately under higher rates of outliers. Why is this the case? There is an important concept to establish here: the rate graphic is not to illustrate how MaMa performs worse under higher outlier percentages, but how cellMCD, DDC, and DI fail to establish any connection under **ALL** outlier rates. Note how precision is stuck at 100% for these three algorithms. Because each algorithm is trained to predict cellwise outliers far from its data center, it fails to determine if the naturally skewed observations found in a log MVN distribution are inliers, which inevitably creates over-sensitive classifications. Thus, the recall is so high, and the precision is so low for lower rates. However, as outlier percentage grows in the study, the trend for precision and F1 increases, making it a more attractive choice on paper, but ultimately not optimal for this type of algorithm. Thus, even though MaMa declines in performance with higher rates, it is very much preferred over these competing alorithms. 

<div style="display: flex; justify-content: center; gap: 10px;">
  <figure style="width: 65%; text-align: center;">
    <img src="/assets/MO4/EffectSizeFigs/Type A/log_MVN-Rho-OutA.png" alt="log_MVN-Rho-OutA-Effect" style="width: 100%;">
    <figcaption>MaMa is the obvious choice when detecting outliers in this distribution</figcaption>
  </figure>
  <figure style="width: 65%; text-align: center;">
    <img src="/assets/MO4/RateFigs/Type A/log_MVN-Rho-OutA.png" alt="log_MVN-Rho-OutA-Rate" style="width: 100%;">
    <figcaption>MVN-trained cellwise algorithms like DDC improve under a 'false' advantage under high outlier rates  </figcaption>
  </figure>
</div>


### Type B Outliers

### Type C Outliers

### Computation Time

## Discussion

## Conclusion

## Awards

BYU held their 2025 Student Research Conference where I could to present my research to! I am estatic to share that I was the selected [winner of my session](https://src.byu.edu/winners/2025) (against 8 other student presenters) from the research I describe here. 