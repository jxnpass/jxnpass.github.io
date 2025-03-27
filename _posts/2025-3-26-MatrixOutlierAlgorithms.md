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

- $W^2$ follows a $\chi_1^2$-distribution (when **X** is MVN).

- If for each observation $i$ in column $j$, 

$$
\begin{equation}
P(W_i^2 > \chi^2_{1, 1 - \alpha}) < \alpha
\end{equation}
$$

where $\alpha$ is the selected significance level for cellwise contamination detection, then cell $x_{ij}$ is classified as an outlier.

The intuition stems from the difference calculation. If removing variable $j$ causes $D_{-j}^2$ to shrink significantly from $D^2$, then $W_i^2$ becomes large and is significant under the $\chi^2_1$ distribution. The algorithm will produce a matrix of binary indicators (`TRUE/FALSE`) suggesting which cells are anomalous.

### Fast DDC

Fast DDC (Detect Deviating Cells) is an algorithm developed by [Peter J. Rousseeuw and Wannes Van Den Bossche in 2017](https://www.tandfonline.com/doi/full/10.1080/00401706.2017.1340909). For Fast DDC to work, the data is first standardized and calculates estimates $z$ based on robust estimates of $\mu$ and $\Sigma$. Cells are then flagged when $z$ surpasses a $\chi^2_1$ distribution. The flagged cells are removed for another round of estimation for bivariate correlations $\rho$. Then they re-impute the cells that are flagged to a best-case prediction value. If cells are deviant from the predicted value, that cell is marked as an outlier.

The primary advantage of Fast DDC is in its name: it proves to be very computationally efficient for larger data and fairly accurate. However, this method can only work when the data derives from a multivariate normal distribution. 

### Cell MCD

Cell MCD, or Cellwise Minimum Covariance Determinant, is based on the framework of Fast DDC to robustly estimate $\mu$ and $\Sigma$, but has added complexities to its computation to make it more concentrated in its identification. Developed by [Peter J. Rousseuw and Jakob Raymaekers in 2024](https://www.tandfonline.com/doi/full/10.1080/01621459.2023.2267777#abstract), it augments Fast DDC by maximizing a multivariate Gaussian likelihood in its estimation of the Mahalanobis distance for each point, then iterates through Concentration, Expectation, and Maximization of the likelihood until convergence (commonly considered C, E, and M steps).

Cell MCD is very accurate and useful for imputing deviating cells (which is not our focus for this research yet) and proves to be a promising detector under Gaussian data. 

### DI

DI stands for Detection Imputation, and is formulated based on two steps. After finding robust estimates of the standardized form of the data, DI utilizes various computations such as LASSO regression to detect cellwise outliers row by row in the Detection D-step, followed by an attempt to impute a corrected value under the Imputation I-step. This process repeats until convergence, or until the changes in the covariance structure are minute. This method is developed by [Peter J. Rousseuw and Jakob Raymaekers in 2020](https://jdssv.org/index.php/jdssv/article/view/18).

Like Cell MCD, DI promises accurate imputation using an EM algorithm based on a Gaussian likelihood. It proves slightly less efficient than Cell MCD and Fast DDC, however.  

### Cell GMM

Cell GMM (Gaussian Mixture Model) is developed by [Zacharria et. al. in 2025](https://www.researchgate.net/publication/383985298_Cellwise_outlier_detection_in_heterogeneous_populations) and is a unique algorithm compared to the previously listed ones as it is specifically designed to handle clusters of multivariate normal data. This method is like Cell MCD, but reconfigures the C-step to classify which rows belong to which cluster. 

Cell GMM proves to be a very strong algorithm in its ability to predict and impute, but has some major downsides to its use. In R programming, cell GMM takes over ten different hyperparameters in order to initialize computing over a dataset. In addition, the cell GMM method is extremely computationally expensive (as we will explore later). It has proven to be very impractical despite its powerful computation. 

## Simulation Results




## Discussion

## Next Steps



