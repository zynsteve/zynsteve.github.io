---
title: Bayes Decision Theory
description: Learning Bayes Decision Theory.
categories:
- Tutorial
tags:
- Pattern Recognition
---


## Bayes Theorem
<block class="block-center">$$P(Y=i|X=x)=\frac{p(x|Y=i)P(Y=i)}{p(x)}=\frac{p(x|Y=i)P(Y=i)}{p(x|Y=0)P(Y=0)+p(x|Y=1)P(Y=1)}$$</block>

## Classifiers and Classification Error
Formally, a classifier is a (measurable) function $\psi:R^d\to\lbrace0, 1\rbrace$ from the feature space Rd into the binary set of labels $\lbrace0, 1\rbrace$. Therefore, a classifier partitions the feature space into two regions.

The classification error is the probability of misclassification:
<block class="block-center">$$\epsilon[\psi] = P(\psi(X) \neq Y)$$</block>

### Conditional Classification Error
$$P(\psi(X)\neq Y|X=x)$$<br/>
$$\eta(X)=P(Y=1|X=x)$$<br/>
$$\epsilon[\psi]=P(\psi(X)\neq Y)=E[P(\psi(X)\neq Y|X)]$$
### Classification Error
### Class-Specific Error Rates
### Testing Error Rates
### Optimal Classification

## Bayes Error
$$\epsilon^*=E[min\lbrace\eta(X),1-\eta(X)\rbrace]$$<br/>
$$\epsilon^*\leq\frac{1}{2}$$

## Bayes Decision Theory
The expected loss upon observing $X=x$ is
<block class="block-center">$$R[\alpha(x)=\alpha_i] = \sum_{j=0}^{c-1}\lambda_{ij}P(Y=j|X=x)$$</block>
This is called the conditional risk given $X=x$

The overall risk is given by
<block class="block-center">$$R=E[R(\alpha(X))]=\int_{x\in R^d}{R(\alpha(x))p(x)}dx$$</block>

To minimize R, we select $\alpha(x)=\alpha_i$ such that $R[\alpha(x)=\alpha_i]$ is minimum, at each value $x\in R^d$. This optimal strategy is called the Bayes decision rule, with corresponding optimal Bayes risk $R^∗$.

## Discriminant Functions
<block class="block-center">$$g_i(x)=\ln p(x|Y=i)+\ln P(Y=i),\quad i=0,1,\cdots,c-1$$</block>

## Gaussian Model
Consider the case where the class-conditional densities are multivariate Gaussian densities:
In other words, <block class="block-center">$$p(x|Y=i)=(2\pi)^{-\frac{d}{2}}|\Sigma_i|^{-\frac{1}{2}}exp(-\frac{1}{2}(x-\mu_i)^T\Sigma_i^{-1}(x-\mu_i))$$</block>
### Nearest Mean Classifier
Case 1: Equal spherical covariance matrices.
<block class="block-center">$$g_i(x)=-\frac{1}{2}\frac{||x-\mu_i||^2}{\sigma^2}+\ln P(Y=i)$$</block>
If the classes are equally-likely, more terms can be dropped and we obtain:
<block class="block-center">$$g_i(x)=-\frac{1}{2}{||x-\mu_i||^2}$$</block>
This is called the optimal Nearest-Mean Classifier.
### Linear Discriminant
### Quadratic Discriminant

## Alternative Distance Measures
### Kolmogorov’s Variational Distance
### Nearest-Neighbor Distance
### Mahalanobis Distance

## F-errors
