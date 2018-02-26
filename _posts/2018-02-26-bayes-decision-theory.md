---
title: Bayes Decision Theory
description: Learning Bayes Decision Theory.
categories:
 - Tutorial
tags:
 - Pattern Recognition
---


## Bayes Theorem
$$P(Y=i|X=x)=\frac{p(x|Y=i)P(Y=i)}{p(x)}=\frac{p(x|Y =i)P(Y =i)}{p(x|Y =0)P(Y =0)+p(x|Y =1)P(Y =1)}$$

## Classifiers and Classification Error
- Formally, a classifier is a (measurable) function $\psi: R^d\to\lbrace0, 1\rbrace$ from the feature space Rd into the binary set of labels $\lbrace0, 1\rbrace$. Therefore, a classifier partitions the feature space into two regions.

- The classification error is the probability of misclassification:
$$\epsilon[\psi]=P(\psi(X)&ne;Y)$$
