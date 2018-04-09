---
title: Perceptrons
description: Learning Perceptrons.
categories:
- Tutorial
tags:
- Pattern Recognition
---


![Perceptrons](https://onlinecourses.science.psu.edu/stat857/sites/onlinecourses.science.psu.edu.stat857/files/lesson10/image_02.gif)
## Adjustable Discriminant Rules
Both parametric and nonparametric classification rules are plug-in rules, that is, they involve some form of distribution estimation using training data.<br/>
We will consider now a different idea:
* Assume a set of discriminants (decision boundaries)
* Search for the discriminant that best fits the data by optimizing some objective criterion (“learning”)

<br/>
This is the basic idea behind many popular “machine learning” classification rules:<br/>
Perceptrons, Support Vector Machines, Neural Networks, Decision Trees

## Rosenblatt’s Perceptron
This was the first adjustable discriminant rule, proposed in the late 50’s by F. Rosenblatt.<br/>
Assume a linear discriminant function
<block class="block-center">$$g_n(x)=a_0+\sum_{i=1}^{d}{a_i x_i}$$</block>
so that the designed classifier is given by
<block class="block-center">$$\psi_n(x)=\begin{cases}1, &\text{if $a_0+\sum{a_i x_i\geq0}$}\\0,&\text{otherwise}\end{cases}$$</block>
Adjust (“learn”) the parameters $a_0, a_1, . . . , a_d$ based on the training data.
![perceptron](/assets/images/post/perceptrons/perceptron.png)

## Augmented Feature Vector
Given the feature vector $x \in R^d$, consider the augmented vector:
<block class="block-center">$$x^\prime=\begin{bmatrix}1\\x\end{bmatrix}\in R^{d+1}$$</block>
so that the perceptron classifier is given by
<block class="block-center">$$\psi_n(x^\prime)=\begin{cases}1, &\text{if $a^Tx^\prime\geq0$}\\0,&\text{otherwise}\end{cases}$$</block>
where $a=[a_0, a_1, ..., a_d]^T\in R^{d+1}$ is the parameter vector.<br/>
Given training data point $(x_i, y_i)$, define likewise the augmented vector $x_i^\prime$, for $i = 1, ..., n$.<br/>
Correct classification of xi happens when
<block class="block-center">$$a^Tx_i^\prime\geq0 \quad \text{if}\quad y_i=1$$</block>
<block class="block-center">$$a^Tx_i^\prime<0 \quad \text{if}\quad y_i=0$$</block>
Trick: flip the sign of $x_i^\prime$ if $y_i=0$ so that<br/>
correct classification of $x_i\Leftrightarrow a^Tx_i^\prime\geq0$<br/>
For convenience, the prime will be omitted from the augmented vector in what follows.
