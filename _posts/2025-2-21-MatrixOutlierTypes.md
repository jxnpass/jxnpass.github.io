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


### Uncontaminated Multivariate Normal Distribution
<iframe src="/assets/MO2/MVN.html"
        width="800" height="650"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

### Type A Cellwise Outliers

* A cell value is much larger or smaller than expected. We set $z$ to impose $X_{ij}$ to be $z \cdot \text{SD}(X_i)$ away from the true value.
<iframe src="/assets/MO2/MVN_TypeA.html"
        width="800" height="650"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

### Type B Cellwise Outliers
A cell is exchanged with a value found within the bounds of $\sim U[\min(X_i), \max(X_i)]$. This scenario adjusts $X_{ij}$ to deviate from the correlation structure enough such that it exceeds the 99th percentile of the Mahalanobis distance of the uncontaminated data.
<iframe src="/assets/MO2/MVN_TypeB.html"
        width="800" height="650"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>

### Type C Cellwise Outliers
A cell value  is replaced by a specific value. This is inspired by the function `generateData` in the `cellWise` package (Raymaekers and Rousseeuw, 2022).
<iframe src="/assets/MO2/MVN_TypeC.html"
        width="800" height="650"
        style="border: 2px solid black; border-radius: 10px;">
</iframe>