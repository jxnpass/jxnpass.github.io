---
title: Algorithmic Forests
description: Random Forests and Bayesian Additive Regression Trees (BART) are both powerful, nonparametric tree-based ensemble methods that predict on both regression and classification tasks. In this post and repository, I explore how they compare with each other regarding model fit, tuning parameters, computation time, and accuracy.  
layout: post

github:
    is_project_page: true
    repository_name: RF-BART-Comparison
    repository_url: https://github.com/jxnpass/RF-BART-Comparison

date: 2024-3-5 17:50:00
---

## Table of Contents
- [Abstract](#abstract)
- [Introduction](#introduction)
- [Fitting Process](#fitting-process)
- [Tuning Parameters](#tuning-parameters)
- [Computation Time](#computation-time)
- [Examples](#examples)
- [Conclusion](#conclusion)

## Abstract
Random forest and Bayesian Additive Regression Trees (BART) are algorithms considered as optimal supervised learning, non-parametric modeling techniques, each offering powerful tools for predictive analytics. I will explore each algorithm process and methodology for handling prediction and classification. Random forests generate numerous trees using tuning parameters that influence the number of trees and the complexity of each decision/split. BART, like Random forest, creates a number of trees, but applies a Markov-Chain Monte-Carlo process to determine an optimal set of trees to be summed (and not averaged like Random Forest). BART additionally incorporates Bayesian priors that govern the depth of each tree and the variety of node (leaf) values. Random forest mitigates overfitting by employing bootstrapping, generating unique datasets for each tree, and refining tree structures through Out-of-Bag (OOB) predictions. In contrast, BART utilizes regularization priors that penalize complex trees, ensuring that default priors favor non-null but small trees to prevent overfitting. We investigate how altering these tuning parameters (and priors) determine fit and prevent overfit on different predictive learning tasks. We apply both approaches to predicting knee angle from a suite of noisy sensors. For our scenarios, I find that BART demonstrates a slight superiority over random forest on 2 of our 3 examples, showcasing enhanced generalization to new observations, and emerges as a more compelling choice for predictive accuracy, despite its computational complexity. However, Random Forest is preferred in scenarios involving unique metrics (see knee sleeve example).

## Introduction
Tree-Ensemble Models (including Random Forest and BART) rely on multiple decision trees to generate predictions. A classic decision tree contains several different branches (TRUE/FALSE decisions) and nodes (endpoints or values) that contribute to explaining some portion of a data problem, such that certain outcomes are expected when running through the tree. Because a tree can have many different combinations of branches/splits, using the tree for this purpose becomes a very viable and flexible method. However, using only one tree may fail in predicting on new data (overfitting). When multiple trees are used in a tree-ensemble model, their combining embodies that original flexibility of one tree AND prevents overfit. These two aspects is what makes Random Forests and BART very powerful tools. 

Random Forest and BART are considered supervised forms of learning. They utilize nonparametric (flexible) approaches to modeling data without requiring the data to follow any particular form. Tree-based ensemble methods can be a reliable friend when your goal is to perform a machine learning task, and you lack the knowledge in (or motivation to research) the topic/data. However, these methods are not recommended for inference-related questions: using numerous trees restricts the interpretability of your data. But, the power from tree-ensemble models are in their ability to estimate predictions individually and combine them. 

Random Forests and BART capitalize on the beauty of utilizing multiple decision tree models to increase predictive accuracy, but have notable differences on how they do so. We will elaborate more on how these two methods generate and fit decision trees on data, how they can each be adjusted using tuning (hyper) parameters, how they relate in computation time, and also how they perform on some different predictive learning tasks. 

## Fitting Process


### Random Forest
### BART

## Tuning Parameters
### Random Forest 
### BART

## Computation Time
### Random Forest 
### BART

## Examples
### Example 0: Simple Simulation
### Example 1: Knee Range of Motion
### Example 2: Diabetes 

## Conclusion

