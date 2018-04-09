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
This is the basic idea behind many popular “machine learning” classification rules:<br/>
Perceptrons, Support Vector Machines, Neural Networks, Decision Trees

## Rosenblatt’s Perceptron
This was the first adjustable discriminant rule, proposed in the late 50’s by F. Rosenblatt.<br/>
Assume a linear discriminant function
<block class="block-center">$$g_n(x)=a_0+\sum_{i=1}^{d}{a_i x_i}$$</block>
so that the designed classifier is given by
<block class="block-center">$$\psi_n(x)=\begin{cases}1, &\text{if $a_0+\sum{a_i x_i\geq0}$}\\0,&\text{otherwise}\end{cases}$$</block>
Adjust (“learn”) the parameters a0, a1, . . . , ad based on the training data.
![perceptron](/assets/images/post/perceptrons/perceptron.png)
