---
title: Bayes Decision Theory
description: Learning Bayes Decision Theory.
categories:
 - Tutorial
tags:
 - Pattern Recognition
---


## Bayes Theorem
$$P(Y = i|X = x) = \frac{p(x|Y = i)P(Y = i)}{p(x)} = \frac{p(x|Y = i)P(Y = i)}{p(x|Y = 0)P(Y = 0) + p(x|Y = 1)P(Y = 1)}$$

## Classifiers and Classification Error
- Formally, a classifier is a (measurable) function $\psi:R^d\to\lbrace0, 1\rbrace$ from the feature space Rd into the binary set of labels $\lbrace0, 1\rbrace$. Therefore, a classifier partitions the feature space into two regions.

- The classification error is the probability of misclassification:
$$\epsilon[\psi] = P(\psi(X) \neq Y)$$

### Conditional Classification Error
$$P(\psi(X) \neq Y|X = x)$$
$$\eta(X) = P(Y = 1|X = x)$$
$$\epsilon[\psi] = P(\psi(X) \neq Y) = E[P(\psi(X) \neq Y|X)]$$
### Classification Error
### Class-Specific Error Rates
### Testing Error Rates
### Optimal Classification

## Bayes Error
$$\epsilon^* = E[min\lbrace\eta(X), 1 - \eta(X)\rbrace]$$<br/>
$$\epsilon^*\leq\frac{1}{2}$$

## Bayes Decision Theory
- The expected loss upon observing $X = x$ is
$$R[\alpha(x) = \alpha_i] = \sum_{j = 0}^{c-1}\lambda_{ij}P(Y = j| X = x)$$<br/>
This is called the conditional risk given $X = x$
- The overall risk is given by
$$R = E[R(\alpha(X))] = \int_{x\in R^d} {R(\alpha(x))p(x)}dx$$
- To minimize R, we select $\alpha(x) = \alpha_i$ such that $R[\alpha(x) = \alpha_i]$ is minimum, at each value $x\in R^d$. This optimal strategy is called the Bayes decision rule, with corresponding optimal Bayes risk $R^∗$.

## Discriminant Functions

## Gaussian Model
### Nearest Mean Classifier
### Linear Discriminant
### Quadratic Discriminant

## Alternative Distance Measures
### Kolmogorov’s Variational Distance
### Nearest-Neighbor Distance
### Mahalanobis Distance

## F-errors
