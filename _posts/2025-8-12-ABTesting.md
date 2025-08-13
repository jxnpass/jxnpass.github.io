---
title: The Holy War of A/B Testing: Frequentists vs Bayesians
description: As I have progressed in to my education and career in statistical inference, I have heard from various professionals, strategy leaders, and peers about how frustrating interpreting statistics results can be. Statistics and data science academics, especially those deep into their fields, have very strong preferences for go-to testing. Here I unpack how both classical and Bayesian statisticians understand uncertainty, handle evidence, and guide decision-making. I'll also provide for R enthusiasts the right playground to perform their own hypothesis tests.
layout: post
tags: [R, Math, Inference]
date: 2025-8-12 7:50:00
---

## Table of Contents
- [Introduction](#introduction)
- [How Frequentists Think](#how-frequentists-think)
- [How Bayesians Think](#how)
- [Proportions](#proportions)
- [Means](#means)
- [Conclusion](#conclusion)

## Introduction

In 2022, NIH researchers published [a 2022 study](https://pmc.ncbi.nlm.nih.gov/articles/PMC9383044/) where they put PhDs, statisticians, and other academics to test something they all should know very well: what is hypothesis testing?

Participants were given a short scenario about statistical significance and asked two seemingly simple follow-up questions. These weren’t trick questions, either—just the kind of thing you might hear in any A/B testing meeting.

Here’s the exact setup they saw:

![fig1](/assets/ABTest/intro.png)

Think you can answer these two questions correctly?

<button type="button" onclick="toggleSpoiler('spoilerContent')">Show Answer</button>
<div id="spoilerContent" style="display:none;">
    Both are "None of the above answers are correct"
</div>

<script>
function toggleSpoiler(id) {
    var content = document.getElementById(id);
    if (content.style.display === 'none' || content.style.display === '') {
        content.style.display = 'block'; // Or 'inline', 'flex', etc., depending on desired layout
    } else {
        content.style.display = 'none';
    }
}
</script>

So, why do so many smart, experienced people get this wrong?
Because terms like p-value, test statistic, and confidence interval—while central to A/B testing—are widely misunderstood, even among professionals.

A/B testing is built to make comparisons, and our brains naturally want to frame those comparisons in everyday language: Is A better than B? By how much? The classical A/B test—often taught in your first statistics course—answers these questions using only the information in your sample. On paper, it’s straightforward.

But when the statistical jargon enters the room, most people’s mental model breaks down. We confuse “unlikely under H₀" with “probable under H₁," and we start interpreting confidence intervals as if they were lottery odds.

This post is your crash course refresher. First, we’ll unpack what p-values and confidence intervals actually mean in the frequentist world. Then, we’ll see how Bayesians approach the same problem—an approach that, depending on your style, might feel either more natural or persuasive.

## How Frequentists Think

Imagine you’ve run an A/B test on two website designs. You collect data and run a statistical test. Out comes a p-value of 0.03. What’s really going on here?

In the frequentist mindset, the p-value tells you: *If there truly were no difference between A and B (the null hypothesis is true), how often would I see a result this extreme—or more extreme—purely by random chance?*

To picture it, think of an alternate universe where you could run your experiment an infinite number of times assuming there is no difference. The results of those imaginary experiments form a bell-shaped “sampling distribution." Your p-value is the proportion of that curve in the “extreme" tail where your observed result lies. If that proportion is tiny, you conclude your data is not consistent with the “no difference" story—and you reject the null hypothesis.

Here’s the catch: rejecting H₀ doesn’t mean you know what’s true instead. You’re essentially saying, This no-difference story doesn’t fit the evidence… but I don’t yet know the full story.

Frequentist methods have a few advantages:

- They’re computationally straightforward and widely applicable.
- Reporting small p-values has become standard in academic publishing.
- Most researchers and analysts at least know what a p-value is supposed to represent.

The biggest stumbling block? Interpretation. People often think a p-value is “the probability H₀ is true" (it’s not), or that a 95% confidence interval means “we are 95% sure the true value lies here" (it doesn’t). The frequentist world is full of subtle rules about what you can and can’t say—and that’s where Bayesians take a very different path.

## How Bayesians Think

Let’s switch gears with a simpler example—a coin flip. You flip a coin, catch it, and cover it. You ask both a Bayesian and a frequentist friend:

“What’s the probability that this coin landed on heads?"

- The Frequentist starts with sharing their experience: “I’ve flipped coins like this before—100 flips, and about 50 were heads. So the long-run probability is 0.5." But when you press them—“Okay, but for this specific coin flip right now?"—they’ll say they can’t give you a probability. From their point of view, the outcome is already fixed as either heads or tails. Probability to them describes long-run frequencies, not single events.
- The Bayesian answers differently. They give their belief, stating “I’ve seen enough fair coins to believe the probability is 50%." They might also quantify how confident they are in that belief—maybe 95% sure based on thousands of previous flips. Then they’d wait for evidence (actual flips from this specific coin) to update that belief. This is the core of Bayesian thinking: start with prior knowledge, bring in new data, and get a posterior—an updated belief about the probability of heads.

In Bayesian statistics, once you have the posterior distribution, you can answer the kinds of questions people want to ask:
- What’s the probability Group A’s conversion rate is higher than Group B’s?
- What’s the probability the true difference lies between an interval X and Y?

That last one is particularly powerful: a Bayesian 95% credible interval isn't restricted the same way a Frequentist is: they really do mean that there is a 95% probability the true value lies within—exactly the kind of plain-English interpretation that frequentists have to dance around by stating their "confidence level".

Of course, there’s a price: Bayesian methods require you to specify a prior belief (which can be controversial), and the math can be computationally heavier. But in exchange, you get results that align much more closely with how humans naturally think about uncertainty.


## Proportions

## Means

## Conclusion


