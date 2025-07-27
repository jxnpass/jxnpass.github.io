---
title: "Outlier Detection Algorithm -- Part 2: Types of Cellwise Outliers"
description: In this post I introduce more of my master's research topics, diving into the different types of outliers found in raw data. 
layout: post

github:
    is_project_page: false
    repository_name: 
    repository_url: 

tags: [Data Science, R, Outlier Detection, Simulations]
date: 2025-2-21 17:50:00
---

## Table of Contents
- [Introduction](#Introduction)
- [Types of Cellwise Outliers](#types-of-cellwise-outliers)
- [Conclusion](#Conclusion)

## Introduction 

Raw data is almost always messy. It often contains errors ranging from incorrect entries to missing values. Failing to handle these errors can disrupt machine learning algorithms and statistical inference, leading to inflated variance and biased estimates. However, erroneous data often follows certain patterns. In [Part 1](/_posts/2025-1-7-MissingValueImputation.md), we discussed how missing data can be Missing At Random, Missing Completely At Random, or Missing Not At Random — all of which relate to the correlation structure of the data.

Outliers, on the other hand, fall into two main categories: casewise and cellwise outliers.

### Casewise Outliers

Casewise outliers occur when an entire row in a dataframe is anomalous. This assumes that most cases come from a certain model distribution, but some deviate from it. These outliers are relatively easy to detect using methods like Cook's or Euclidean Distance. A large body of research already exists on detecting these types of outliers.

### Cellwise Outliers

Cellwise outliers occur when a single cell within a row is anomalous. These are harder to detect and more common in research data. They often result from data entry errors or recording issues. Research into detecting cellwise outliers is relatively recent, with significant advancements over the last decade by researchers like Rousseeuw and Raymakers. In [Part 3](/_posts/2025-3-26-MatrixOutlierAlgorithms.md), we will explore these methods and introduce a new approach.

<p align="center">
<img style="width: 50%" src="/assets/MO2/outliergenres.png" alt="outliers">
</p>

## Types of Cellwise Outliers

Cellwise outliers are tricky to detect because they only stand out in multi-dimensional settings or when reduced to two dimensions. Without actively looking for them, they can go unnoticed and compromise model performance and statistical inference.

We’ll explore different types of cellwise outliers using a three-dimensional dataset generated from a multivariate normal distribution. The plot below illustrates the dataset’s strong positive correlation between $X_1$, $X_2$, and $X_3$, which makes detecting cellwise outliers easier despite potential issues with linear models.

<iframe src="/assets/MO2/MVN.html"
        width="800" height="800"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

### Type A: Z-Score
A cell value is much larger or smaller than expected. We define $z$ as the number of standard deviations ($\text{SD}(X_i)$) that $X_{ij}$ deviates from the true value.
* Example: A researcher records subjects’ weights, but some are recorded in pounds instead of kilograms.

<iframe src="/assets/MO2/MVN_TypeA.html"
        width="800" height="800"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

### Type B: Mahalanobis Quantile
A cell value is exchanged with a value within the range of $\sim U[\min(X_i), \max(X_i)]$, causing it to exceed the 99th percentile of the Mahalanobis distance of the uncontaminated data.
* Example: A computer program accidentally shuffles values in one of the columns, disrupting the correlation structure.

<iframe src="/assets/MO2/MVN_TypeB.html"
        width="800" height="800"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

### Type C: Cellwise Replacement
A cell value is replaced by a specific value. This is based on the function `generateData` in the `cellWise` package (Raymaekers and Rousseeuw, 2022).
* Example: A computer program randomly replaces some values in a column with 3 — even though some original values were already 3.
<iframe src="/assets/MO2/MVN_TypeC.html"
        width="800" height="800"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

## Conclusion
We explored the difference between cellwise and casewise outliers, along with the different types of cellwise outliers and how they appear in real-world data. In [Part 3](/_posts/2025-3-26-MatrixOutlierAlgorithms.md), we will examine how our new algorithm compares to leading methods for detecting cellwise outliers.



