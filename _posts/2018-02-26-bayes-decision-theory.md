---
title: Bayes Decision Theory
description: Learning Bayes Decision Theory.
categories:
- Tutorial
tags:
- Pattern Recognition
---


![Bayes Decision Theory](https://onlinecourses.science.psu.edu/stat857/sites/onlinecourses.science.psu.edu.stat857/files/lesson10/image_02.gif)
## Class-Conditional Densities
The relative frequencies of each label as a function of predictor values are given by the class-conditional densities $p(x|Y=i)$, for $i=0,1$.
![Class-Conditional Densities](https://www.byclb.com/TR/Tutorials/neural_networks/Ch_4_dosyalar/image001.gif)

## Posterior Probabilities
Using Bayes’ theorem, we can start from the prior probabilities and class-conditional densities and find the posterior probability of $Y=i$ given that $X=x$ has been observed, for $i=0,1$:
<block class="block-center">$$P(Y=i|X=x)=\frac{p(x|Y=i)P(Y=i)}{p(x)}=\frac{p(x|Y=i)P(Y=i)}{p(x|Y=0)P(Y=0)+p(x|Y=1)P(Y=1)}$$</block>
Posterior probabilities are not probability densities (e.g., they do not integrate to 1) but are simply probabilities (in particular, they are always between 0 and 1).
![Posterior Probabilities](https://www.byclb.com/TR/Tutorials/neural_networks/Ch_4_dosyalar/image006.gif)

## Classifiers and Classification Error
Formally, a classifier is a (measurable) function $\psi:R^d\to\lbrace0, 1\rbrace$ from the feature space Rd into the binary set of labels $\lbrace0, 1\rbrace$. Therefore, a classifier partitions the feature space into two regions.

The classification error is the probability of misclassification:
<block class="block-center">$$\epsilon[\psi] = P(\psi(X) \neq Y)$$</block>

### Conditional Classification Error
The conditional classification error is the error at a particular observed value of $X$: $P(\psi(X)\neq Y|X=x)$<br/>
Notice that
<block class="block-center">$$P(\psi(X)\neq Y|X=x)=P(\psi(X)=0,Y=1|X=x)+P(\psi(X)=1,Y=0|X=x)$$
$$=I_{\psi(X)=0}P(Y=1|X=x)+I_{\psi(X)=1}P(Y=0|X=x)$$
$$=I_{\psi(X)=0}\eta(X)+I_{\psi(X)=1}(1-\eta(X))$$</block>
where the posterior probability function $\eta : R^d \to [0, 1]$,
<block class="block-center">$$\eta(X)=P(Y=1|X=x)$$</block>
The classification error is the “average” conditional classification error:
<block class="block-center">$$\epsilon[\psi]=P(\psi(X)\neq Y)$$
$$=\int_{x\in R^d}P(\psi(X)\neq Y|X=x)p(x)dx$$
$$=E[P(\psi(X)\neq Y|X)]$$</block>
Therefore, knowing the error at each point $x\in R^d$ of the feature space, plus the “weight” $p(x)$, is enough to determine the overall classification error.
### Classification Error
<block class="block-center">$$\epsilon[\psi]=\int_{x\in R^d}P(\psi(X)\neq Y|X=x)p(x)dx$$
$$=\int_{x\in R^d}(I_{\psi(X)=0}\eta(X)+I_{\psi(X)=1}(1-\eta(X)))p(x)dx$$
$$=\int_{x|\psi(x)=0}\eta(X)p(x)dx+\int_{x|\psi(x)=1}(1-\eta(X))p(x)dx$$</block>
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
Case 2: Equal arbitrary covariance matrices.
### Quadratic Discriminant

## Alternative Distance Measures
### Kolmogorov’s Variational Distance
### Nearest-Neighbor Distance
The Nearest-Neighbor Distance is given by
<block class="block-center">$$\epsilon^*=E[2\eta(x)(1-\eta(x))]$$</block>
The following distribution-free inequalities hold:
<block class="block-center">$$\epsilon^*\leq \epsilon_{NN}\leq 2\epsilon^*(1-\epsilon^*)$$</block>
Since 0 ≤ 2η(x)(1 − η(x)) ≤ 1, for all x, we have
<block class="block-center">$$0\leq\epsilon_{NN}\leq\frac{1}{2}$$</block>
Furthermore, it is clear that
<block class="block-center">$$\epsilon_{NN}=0\Leftrightarrow\eta(x)\in\lbrace0,1\rbrace w.prob.1\Leftrightarrow\epsilon^*=0$$</block>
<block class="block-center">$$\epsilon_{NN}=\frac{1}{2}\Leftrightarrow\eta(x)=\frac{1}{2}w.prob.1\Leftrightarrow\epsilon^*=\frac{1}{2}$$</block>
so $\epsilon_{NN}$ carries plenty of information about $\epsilon^*$.
### Mahalanobis Distance
The Mahalanobis distance, defined previously as
<block class="block-center">$$\delta=\sqrt{(\mu_1-\mu_0)^T\Sigma^{-1}(\mu_1-\mu_0)}$$</block>
is a an alternative distance measure that is related to the Bayes error.
## F-errors
