---
title: "Strong Youth Project"
description: I highlight my contributions on researching how different coaching cues impact young athletes' performance in a single-leg triple hop test. By comparing control, internal, and external focus cues utilizing experimental analysis techniques, the study found that external cues led to greater improvements in jump distance, showing it as an estimated 10.4% performance booster for enhancing athletic performance and coaching. 
layout: post

github:
    is_project_page: true
    repository_name: StrongYouthProject
    repository_url: https://github.com/jxnpass/StrongYouthProject

date: 2024-10-16 17:50:00
---

## Table of Contents
- [Abstract](#Abstract)
- [Introduction](#Introduction)
- [Methods and Results](#methods-and-results)
- [Conclusion](#Conclusion)

## Abstract
This study explored how different coaching cues—specifically, internal (focusing on body movements) and external (focusing on an object beyond their reach)—impact young athletes' performance on a single-leg triple hop test. Thirty-nine athletes, aged 10-17, were divided into three groups: a control group, an internal cue group, and an external cue group.

Each athlete completed three practice trials before receiving instruction relevant to their group. Those in the internal cue group received coaching emphasizing arm movements, while the external cue group was told to aim beyond a cone. The control group watched a video that was unrelated. Performance was measured by the change in jump distance from before to after receiving the cues, with angles at the hip, knee, and ankle analyzed using motion capture.

Univariate ANOVA results showed that the external cue group had significantly greater improvements in jump distance than both the control (by 8.3%) and internal cue (by 7.1%) groups (p = 0.0059 and p = 0.0148, respectively). These improvements were similar for both males and females. Additionally, secondary findings revealed moderate correlations between changes in joint angles, particularly the ankle and knee (r = 0.70). The study suggests that using external cues could be a promising coaching approach to boost performance and potentially reduce injury risk in young athletes. Multivariate ANOVA (MANOVA) infers that groups overall kinematics among treatment groups also differed (p = 0.004), particularly pairwise comparisons between external and interal cues (p = 0.010) and potentially between external and control (p = 0.071).

## Introduction

BYU sponsors its Exercise Science program, its faculty, and select students, to host the (Strong Youth Project)[https://exsc.byu.edu/the-strong-youth-project-homepage] (SYP), with its focus to promote positive experiences in sports for youth. Encouraging children's sports fights health concerns like obesity, diabetes, depression, and other common challenges in society. With a focus on implementing evidence-based insights in athletic performance, SYP sponsors various projects for both children and youth coaches to benefit from. 

The SYP team reached out to many other departments to participate and develop their research, one of which was the statistics department. My professor and I were called in to analyze a dataset related to different youths' reception to training cues, particularly for an exercise called the single-leg triple-hop. As demonstrated in the video below, the subject is to jump as far as they can in three jumps using one leg of their choice. Motion capture technology, called [OpenCap](https://www.opencap.ai/), videos each subject and renders a 3D frame of their body. It also calculates metrics based on their kinematics (that are important to our study), including their hip, knee, and ankle angles, and the amount of time their foot is on the ground between jumps (called stance time). The experiment included three types of treatments, or coaching cues, to teach the youth: a video unrelated to the exercise (control), a training demonstration on good jumping form (internal), and an object to jump too that was beyond their reach (external). 

![motioncapture](/assets/SYP/triplehopmotioncapture.gif)

This analysis aims to answer the following questions related to the triple-hop experiment:
1. Do the three different coaching cues differ in triple-hop jumping distances?
2. Do the three different coaching cues influence jumping techniques (kinematics)?
3. What is the relationship between coaching cues and changes in kinematics?

## Methods and Results

It is important to note too that this case will be considering five separate variables in the forms of percent change, namely the jump distance, ankle, hip, and knee angle changes, and the stance time. That means I had to learn and explore different multivariate methods. My process of working through this data was by first exploring the data itself (EDA), and following that then performed univariate ANOVA, multivariate ANOVA, and LDA (also known as linear discriminant analysis), with the latter two being more unfamiliar to me at this point in my education.  

### EDA

The following figure below visualizes how each variable of percent change differed among treatment groups. Notably, we see that the external group had an average 10.4% jump distance increase, compared to the control at 2.1% and internal at 3.4%. This was a promising indicator that external training seems to influence the participants' abilities to jump further than they previously could: in sports performance, a 10% increase in any exercise is certainly impressive. When also visualizing ankle, hip, knee, and stance time, we could also make visual inference about group differences here, but notice how varied each point is. These variables tended to be much more volatile than jump distance, which may make significance among treatment groups harder to detect. 

![EDA1](/assets/SYP/EDA.png)

To answer questions about each variable influence amongst each other, I also explored creating a correlation matrix among each of the response variables, as seen below. I find correlation matrices a popular tool for understanding data quick (assuming these variables are continuous and linear). Also, correlations are typically widely understood among many, including the exercise science team, and so demonstrating this graphic really excited them. 

![EDA2](/assets/SYP/CorrMatPercent.png)

I promise I am not overstating this when I say that when I showed the correlation matrix to them, they stared and discussed it for 15 minutes. Not that it was confusing, but the first time they've been able to see how kinematics related to each other. They also started discussing theories among three angle connections related to anatomy that are beyond topics that I know, but it was very interesting to see how they connected my data analysis to their field of study so cleanly -- all of it was amazing to sit in and experience. One of these theories that circulated and finding were about the strong 0.70 correlation between knee and ankle angle, specifically how diving down into a deeper stance in your knee also flexes your ankle drive more. In addition, the hip angle with a mild correlation of 0.32 may relate to how deeper hip flexion drives your jump distance a little bit more. 

I share these because sometimes statistical analysis may get data scientists, statisticians, and like-groups excited, but for other backgrounds, they get lost quickly. Using data visualization in research is an important tool to connect audiences to your modeling. 

### ANOVA

This section aims to answer how the coaching cues differ with jump distance purely. As noted already, the external group had a 10.4% change in jump distance, which was 8.3% higher than the control group and 7.1% higher than the internal group. 

The ANOVA model determines differences among group means, and as such, determined that treatment indeed was significant (p = 0.005). The ANOVA also considered other variables that we don't discuss fully in this blog, namely sex, the initial jump distance, a treatment-sex interaction term, and a sex:initial jump distance interaction term. The ANOVA component of this code is featured below in R. None of these terms were considered significant, but they do help control for potential bias and answer some of our sub-questions. 

```
lm_jump <- lm(JumpDistanceChange ~ Treatment*Sex + Sex*AVGPreJumpDistance, data = syp) 
# note that * uses the first term, then the second, then the interaction. 
anv_jump <- anova(lm_jump) 
print(anv_jump) # treatment at p = .005
```

In addition, we are interesting in doing pairwise comparisons among treatment groups. This will tell us about the effect of one treatment group and how it differs to another. ```TukeyHSD()``` is a great function for computing these pairwise differences. The graph below essentially calculates these pairwise differences (for all variables of interest), and reveals how some of these comparisons hang above the zero line, indicating treatment effects among group. With a bonferroni p-value adjustment, the external-internal and external-control pairwise comparisons are significant (p = 0.0059 and p = 0.0148). Internal-control is not significantly different (p = 1). Note that I did the pairwise comparisons for all groups, but only jump distance has significant comparisons above zero. 

![PWs](/assets/SYP/PWEffectsGraph.png)

## MANOVA

## LDA

## Conclusion

You can check out more of this project on this [Instagram post](https://www.instagram.com/p/DBkf_LqNh0H/). Academic paper pending. 


