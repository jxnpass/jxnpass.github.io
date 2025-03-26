---
title: "Outlier Detection Algorithm -- Part 3: Methods for Detecting Cellwise Outliers"
description: In this post I introduce the main algorithm to define my master's research project, called MaMa (for Marginalized Mahalanobis), as well as exploring how competing algorithms classify cellwise outliers compared to ours.
layout: post

github:
    is_project_page: false
    repository_name: 
    repository_url: 

tags: [Data Science, R, Outlier Detection, Simulations]
date: 2025-3-26 7:50:00
---

## Table of Contents
- [Introduction](#introduction)
- [Methods](#methods)
- [Simulation Results](#simulation-results)
- [Discussion](#discussion)
- [Next Steps](#next-steps)

## Introduction
In this article, I add upon [Part 2](/_posts/2025-2-21-MatrixOutlierTypes.md) of the Outlier Detection Algorithm Series by exploring the various methods aimed towards accurately detecting cellwise outliers within a given dataset. We detail how each algorithm works, starting with a more expanded description of how our newly developed method Marginalized Mahalanobis (or MaMa). We then review the accuracy of each method in classifying cellwise outliers. We will see how MaMa is able to handle various scenarios outside of the multivariate normal distribution that the other algorithms struggle to handle. 

## Methods

In this section, I introduce our method MaMa, followed by five additional methods that have been developed within the last few years. 

### Marginalized Mahalanobis

Marginalized Mahalanobis (MaMa) is a method recently theorized by my advisor [William Christensen](https://tofu.byu.edu/docs/index.html) and I developed in R programming. The steps involved is as follows:

We start by calculating the squared Mahalanobis distance for every row in $\textbf{X}$ to get $D^2$:

$$
\begin{equation}
D^2 = (\boldsymbol x - \boldsymbol\mu)^T \boldsymbol\Sigma^{-1} (\boldsymbol x - \boldsymbol\mu)
\end{equation}
$$

The Mahalanobis distance formula computes the distance between observations within the data and the mean $\boldsymbol\mu$, also taking into account the correlation structure of the dat $\Sigma$. The significance of incorporating $\Sigma$ is to account for extreme values consistent with trends in the data to have a lower $D^2$ than any extreme values that are clearly separated from those trends. 

For every column/variabel $j$ in $\textbf{X}$.


- Compute the Mahalanobis distance excluding $x_j$, $\mu_j$, and $\Sigma_{j}$ to get $D_{-j}^2$:  

$$
\begin{equation}
D_{-j}^2 = (\boldsymbol{x}_{-j} - \boldsymbol{\mu}_{-j})^T \boldsymbol{\Sigma}_{-j}^{-1} (\boldsymbol{x}_{-j} - \boldsymbol{\mu}_{-j})
\end{equation}
$$

- Compute the Marginalized Mahalanobis:

$$
\begin{equation}
W^2 = D^2 - D_{-j}^2
\end{equation}
$$

- $W^2$ follows a $\chi_1^2$-distribution with 1 degree of freedom (when **X** is MVN).

- If for each observation $i$ in column $j$, 

$$
\begin{equation}
P(W_i^2 > \chi^2_{1, 1 - \alpha}) < \alpha
\end{equation}
$$

where $\alpha$ is the selected significance level for cellwise contamination detection, then cell $x_{ij}$ is classified as an outlier.

The intuition stems from the difference calculation. If removing variable $j$ causes $D_{-j}^2$ to shrink significantly from $D^2$, then $W_i^2$ becomes large and is significant under the $\chi^2_1$ distribution. The algorithm will produce a matrix of binary indicators (`TRUE/FALSE`) suggesting which cells are anomalous.





## Simulation Results

## Discussion

## Next Steps



