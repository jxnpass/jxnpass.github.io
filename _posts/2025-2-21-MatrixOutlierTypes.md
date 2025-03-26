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

Raw data is almost always messy. It comes with plenty of errors ranging between the data being recorded incorrectly to missing completely. Not handling these errors may make machine learning algorithms or statistical inference problematic, with inflated variance in its estimation or  However, erroneous data may have certain patterns to its complications. In [Part 1](/_posts/2025-1-7-MissingValueImputation.md), we discussed how missing data can be Missing At Random, Missing Completely At Random, or Missing Not At Random, which all of it relates to the correlation structure of the data. Outlier data, on the other hand, comes in two different genres, namely casewise and cellwise outliers. 

### Casewise Outliers

Casewise outliers are when an entire row within a dataframe is anomalous. It assumes that most cases were drawn from a certain model distribution but some other cases were not. These can be easily detected with various methods, namely Cook's Distance, Euclidean Distance, or _. Plenty of research has been conducted already to detect these types of outliers. 

### Cellwise Outliers
Cellwise outliers are outliers where one cell within a row is anomalous. These are much harder to detect, and more common among research data. These occur likely when a computer has recording issues, or data entry workers make mistakes imputing research data. Most research exploring detecting these outliers are very recent; within the last 10 years, the most promising methods to detect these outliers have been developed by statistical researchers like Rousseeuw and Raymakers. I explore these methods and introduce our new method in Part 3.

<p align="center">
<img style="width: 50%" src="/assets/MO2/outliergenres.png" alt="outliers">
</p>

## Types of Cellwise Outliers

Cellwise outliers are unique in that they only stand out visually either within a multi-dimensional setting, or when the cell's column is marginalized to be within a two-dimensional framework. If you don't know to look for them, they could go completely undetected, and it will corrupt parts of your model and/or statistical inferences. In this article, we explore different types of cellwise outliers and how they can be seen when the data is three-dimensional (i.e. the dataframe has three columns). 

As a base case, we start with a three-dimensional multivariate normal distribution. The dataset, represented in a three-dimensional plot below. The strong positive direction from the origin indicates that the correlation structure incorporates high collinearity between $X_1$, $X_2$, and $X_3$. As a consequence to outlier detection, higher collinearity makes classifying cellwise outliers easier, despite sometimes being problematic for linear models. 

<iframe src="/assets/MO2/MVN.html"
        width="800" height="650"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

### Type A: Z-Score

A cell value is much larger or smaller than expected. We set $z$ to impose $X_{ij}$ to be $z \cdot \text{SD}(X_i)$ away from the true value.
* Example: a researcher records data of the weight of subjects, and records some of the weights in lbs instead of kg. 

<iframe src="/assets/MO2/MVN_TypeA.html"
        width="800" height="650"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

### Type B: Mahalanobis Quantile
A cell is exchanged with a value found within the bounds of $\sim U[\min(X_i), \max(X_i)]$. This scenario adjusts $X_{ij}$ to deviate from the correlation structure enough such that it exceeds the 99th percentile of the Mahalanobis distance of the uncontaminated data.
* Example: a computer program accidentally shuffles some of the observations in one of the data columns. It doesn't necessarily ruin 

<iframe src="/assets/MO2/MVN_TypeB.html"
        width="800" height="650"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

### Type C: Cellwise Replacement
A cell value  is replaced by a specific value. This is inspired by the function `generateData` in the `cellWise` package (Raymaekers and Rousseeuw, 2022).
* Example: a computer program randomly replaces some of the values within a column to be 3 (but some of the cells were actually 3).
<iframe src="/assets/MO2/MVN_TypeC.html"
        width="800" height="650"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

## Conclusion
We explored the difference between cellwise and casewise outliers, as well as the styles of cellwise outliers and where they may occur in real world data. This article sets up our part 3 of the matrix outlier series in exploring our new algorithm competes with leading methods for cellwise detection. 




