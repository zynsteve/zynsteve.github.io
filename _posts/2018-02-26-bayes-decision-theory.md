---
title: Bayes Decision Theory
categories:
- Tutorial
tags:
- Pattern Recognition
---


## Class-Conditional Densities
The relative frequencies of each label as a function of predictor values are given by the class-conditional densities $p(x|Y=i)$, for $i=0,1$.
![Class-Conditional Densities](https://www.byclb.com/TR/Tutorials/neural_networks/Ch_4_dosyalar/image001.gif)
<!-- more -->

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
Using the previous formulas, one can further develop the classification error as:
<block class="block-center">$$\epsilon[\psi]=\int_{x\in R^d}P(\psi(X)\neq Y|X=x)p(x)dx$$
$$=\int_{x\in R^d}(I_{\psi(X)=0}\eta(X)+I_{\psi(X)=1}(1-\eta(X)))p(x)dx$$
$$=\int_{\lbrace x|\psi(x)=0\rbrace}\eta(X)p(x)dx+\int_{\lbrace x|\psi(x)=1\rbrace}(1-\eta(X))p(x)dx$$</block>
From Bayes theorem,
<block class="block-center">$$P(Y=i|X=x)=\frac{p(x|Y=i)P(Y=i)}{p(x)}$$</block>
we have
<block class="block-center">$$P(Y=i|X=x)p(x)=p(x|Y=i)P(Y=i)$$</block>
Therefore,
<block class="block-center">$$\eta(x)p(x)=p(x|Y=1)P(Y=1)$$
$$(1-\eta(x))p(x)=p(x|Y=0)P(Y=0)$$</block>
Replacing these into the previous formula yields an alternative equation for the classification error:
<block class="block-center">$$\epsilon[\psi]=\int_{\lbrace x|\psi(x)=0\rbrace}P(x|Y=1)P(Y=1)dx+\int_{\lbrace x|\psi(x)=1\rbrace}P(x|Y=0)P(Y=0)dx$$</block>

### Class-Specific Error Rates
We can rewrite the previous equation as:
<block class="block-center">$$\epsilon[\psi]=(1-c)\epsilon^0[\psi]+c\epsilon^1[\psi]$$</block>
where $c=P(Y=1)$, and
<block class="block-center">$$\epsilon^0[\psi]=\int_{\lbrace x|\psi(x)=1\rbrace}P(x|Y=0)dx$$
$$\epsilon^1[\psi]=\int_{\lbrace x|\psi(x)=0\rbrace}P(x|Y=1)dx$$</block>
are the class-specific error rates. Given $\psi$, these error rates do not depend on the prior probabilities c and $1 − c$, while the overall error $\epsilon^0[\psi]$ clearly does.

### Testing Error Rates

### Optimal Classification
(DGL Theorem 2.1) The classifier with minimal error is <block class="block-center">$$\psi^∗(x) = argmax_i P(Y=i|X=x)=I_{\eta(x)>\frac{1}{2}}.$$</block>
This is the MAP (Maximum A-Posteriori) classifier, more commonly known as the Bayes classifier.<br/>
By Bayes theorem, we have, equivalently,
<block class="block-center">$$\psi^∗(x) = argmax_i P(x|Y=i)P(Y=i)$$</block>

## Bayes Error
The error of the Bayes classifier
<block class="block-center">$$\epsilon^*=\epsilon[\psi^*]$$</block>
is a fundamental quantity in PR, known as the Bayes error.<br/>
Note that the Bayes classifier is given by
<block class="block-center">$$\psi^*(x)=\begin{cases}1, \eta(x)>1-\eta(x)\quad(\eta(x)>\frac{1}{2})\\0,\eta(x)\leq1-\eta(x)\quad(\eta(x)\leq\frac{1}{2})\end{cases}$$</block>
Therefore
<block class="block-center">$$\epsilon^*=\int_{\eta(x)<1-\eta(x)}\eta(X)p(x)dx+\int_{\eta(x)\geq1-\eta(x)}(1-\eta(X))p(x)dx$$
$$=E[min\lbrace\eta(X),1-\eta(X)\rbrace]$$</block>
In particular, we always have $\epsilon^*\leq\frac{1}{2}$.

## Bayes Decision Theory
Suppose that upon observing X = x one takes an action α(x) in a finite set of a possible actions<br/>
<block class="block-center">$$\alpha(x)\in\lbraceα_0,α_1,...,α_{a−1}\rbrace$$</block>
Suppose there are c states of nature (i.e., classes), $Y \in\lbrace0,1,...,c−1\rbrace$. Each action incurs a loss <block class="block-center">$λ_{ij} = \text{cost of taking action αi when true state of nature is j}$</block>
Action $i$ may be simply deciding that the true state of nature is $i$, but we may have $a>c$, in which case one of the extra actions might be rejecting to make a decision.<br/>
The losses indicate, for example, the cost of making incorrect decisions.
The expected loss upon observing $X=x$ is
<block class="block-center">$$R[\alpha(x)=\alpha_i] = \sum_{j=0}^{c-1}\lambda_{ij}P(Y=j|X=x)$$</block>
This is called the conditional risk given $X=x$.<br/>
The overall risk is given by
<block class="block-center">$$R=E[R(\alpha(X))]=\int_{x\in R^d}{R(\alpha(x))p(x)}dx$$</block>
To minimize R, we select $\alpha(x)=\alpha_i$ such that $R[\alpha(x)=\alpha_i]$ is minimum, at each value $x\in R^d$. This optimal strategy is called the Bayes decision rule, with corresponding optimal Bayes risk $R^∗$.<br/>
In the special case that a = c = 2, that is, there are two classes and two actions, we have
<block class="block-center"></block>$$R[\alpha(X)=\alpha_0]=\lambda_{00}P(Y=0|X=x)+\lambda_{01}P(Y=1|X=x)\quad (I)$$
$$R[\alpha(X)=\alpha_1]=\lambda_{10}P(Y=0|X=x)+\lambda_{11}P(Y=1|X=x)\quad (II)$$</block>
We decide for action $\alpha_0$ if $(II) > (I)$, that is, if
<block class="block-center">$$(\lambda_{10}-\lambda_{00})P(Y=0|X=x)>(\lambda_{01}-\lambda_{11})P(Y=1|X=x)$$</block>
Applying Bayes theorem (and assuming that $lambda_{10} > lambda_{00}$) allows us to write
<block class="block-center">$$\frac{p(x|Y=0)}{p(x|Y=1)}>\frac{\lambda_{01}-\lambda_{11}}{\lambda_{10}-\lambda_{00}}\frac{P(Y=1)}{P(Y=0)}$$</block>
that is, we decide for action $\alpha_0$ if the likelihood ratio on the left is larger than the given threshold.<br/>
The case where
<block class="block-center">$$\lambda_{00}=\lambda_{11}=0$$
$$\lambda_{10}=\lambda_{01}=1$$</block>
is called the $0-1$ loss case. This is the case that we had considered before, if action $\alpha_i$ is simply deciding that the state of nature is $i$, for $i=0,1$.

## Discriminant Functions
A classifier can be specified through a set of discriminant functions $\lbrace g_i(x)|i = 0, 1, . . . , c − 1\rbrace$ as:<br/>
<block class="block-center">$$\psi(x)=argmax_i g_i(x)$$</block>
The $i−th$ decision region is determined by
<block class="block-center">$$g_i(x)>g_j(x),\quad\text{for all}\quad i\neq j$$</block>
The loci of ties among largest discriminant functions determine the decision surfaces.
<block class="block-center">$$g_i(x)=\ln p(x|Y=i)+\ln P(Y=i),\quad i=0,1,\cdots,c-1$$</block>
A set of discriminant functions determines a unique classifier, but the converse is not true: the same classifier can be determined by multiple sets of discriminant functions.<br/>
Monotonic transformations to the discriminant functions do not alter the classifier.<br/>
For example, it is often useful to take logs and represent the Bayes classifier through the discriminant functions
<block class="block-center">$$g_i(x)=\ln p(x|Y=i)+\ln P(Y=i),\quad i=0,1,...,c−1$$</block>
In the two-category case, we can define a single discriminant function
<block class="block-center">$$g(x)=g_1(x)−g_0(x)$$</block>
In which case the classifies is determined by
<block class="block-center">$$g(x)>0\Rightarrow\psi(x)=1$$
$$g(x)\leq0\Rightarrow\psi(x)=0$$</block>
For example, for the Bayes classifier
<block class="block-center">$$g(x)=P(Y=1|X=x)-P(Y=0|X=x)$$
$$g(x)=\ln\frac{p(x|Y=1)}{p(x|Y=0)}+\ln\frac{P(Y=1)}{P(Y=0)}$$</block>

## Gaussian Model
Consider the case where the class-conditional densities are multivariate Gaussian densities:
<block class="block-center">
$$p(x|Y=i)\sim  N_d(\mu_i,\Sigma_i),\quad i=0,1,...,c−1$$</block>
In other words,
<block class="block-center">$$p(x|Y=i)=(2\pi)^{-\frac{d}{2}}|\Sigma_i|^{-\frac{1}{2}}exp(-\frac{1}{2}(x-\mu_i)^T\Sigma_i^{-1}(x-\mu_i))$$</block>

### Nearest Mean Classifier
Case 1: Equal spherical covariance matrices.<br/>
In this case,
<block class="block-center">$$\Sigma_i=\sigma^2I_d\Rightarrow\Sigma^{−1}=\frac{1}{\sigma^2}I_d,\quad i=0,1,...,c−1$$</block>
The constant term $\ln|\Sigma_i|=−2d\ln\sigma$ can be dropped, leading to
<block class="block-center">$$g_i(x)=-\frac{1}{2}\frac{||x-\mu_i||^2}{\sigma^2}+\ln P(Y=i)$$</block>
If the classes are equally-likely, more terms can be dropped and we obtain:
<block class="block-center">$$g_i(x)=-\frac{1}{2}{||x-\mu_i||^2}$$</block>
This is called the optimal Nearest-Mean Classifier.
![Nearest Mean Classifier](https://ask.julyedu.com/uploads/answer/20150203/212bec42a04acaf238e72b613dba8371.png)

### Linear Discriminant
Case 2: Equal arbitrary covariance matrices.<br/>
In this case,
<block class="block-center">$$\Sigma_i=\Sigma,\quad i=0,1,...,c−1$$</block>
Once again, the constant term $\ln|\Sigma_i|=\ln|\Sigma|$ can be dropped, resulting in
<block class="block-center">$$g_i(x)=−\frac{1}{2}(x−\mu_i)^T\Sigma^{−1}(x−\mu_i) + \ln P(Y=i)$$</block>
This is apparently a quadratic discriminant; however the quadratic term is $x^T\Sigma^{−1}x$, which is constant and can be dropped, leading to a linear discriminant:
<block class="block-center">$$g_i(x)=a_i^Tx+b_i$$</block>
In the case c = 2, the single discriminant is given by:
<block class="block-center">$$g_i(x)=a^Tx+b$$</block>
Clearly, the equation $g(x) = 0$ defines a hyperplane decision boundary.<br/>
If the classes are equally-likely, then the hyperplane is given by:
<block class="block-center">$$g(x)=a^T(x−x_0)=0$$</block>
where
<block class="block-center">$$a=\Sigma^{−1}(\mu_1−\mu_0)$$
$$x_0 = \frac{1}{2}(μ_1+μ_0)$$</block>
that is, the hyperplane must pass through the midpoint between the means, but it is not in general perpendicular to the axis joining the means (as was true for the nearest-mean classifier in case 1), because $\Sigma^{−1}(\mu_1−\mu_0)$ is not in general parallel to $(\mu_1−\mu_0)$, unless the latter is an eigenvector of $\Sigma^{−1}$ (and thus of $\Sigma$).<br/>
Using the properties of the Gaussian distribution,
<block class="block-center">$$g(X)|Y=0\sim a^TX+b|Y=0\sim N(a^Tμ_0+b,a^T\Sigma a)$$
$$g(X)|Y=1\sim a^TX+b|Y=1\sim N(a^Tμ_1+b,a^T\Sigma a)$$</block>
It follows that
<block class="block-center">$$\epsilon^0[\psi^*]=P(g(X)>0|Y=0)=\Phi\left(\frac{a^T\mu_0+b}{\sqrt{a^T\Sigma a}}\right)$$
$$\epsilon^1[\psi^*]=P(g(X)\leq0|Y=1)=\Phi\left(-\frac{a^T\mu_1+b}{\sqrt{a^T\Sigma a}}\right)$$</block>
where $\Phi(x)$ is the CDF of a $N(0,1)$ distribution.<br/>
Substituting the values of a and b leads to
<block class="block-center">$$\epsilon^0[\psi^*]=\Phi\left(\frac{-\frac{1}{2}\delta^2+k}{\delta}\right)$$
$$\epsilon^1[\psi^*]=\Phi\left(\frac{-\frac{1}{2}\delta^2-k}{\delta}\right)$$</block>
where
<block class="block-center">$$k=\ln(P(Y=1)/P(Y=0))$$
$$\delta=\sqrt{(\mu_1−\mu_0)^T\Sigma^{−1}(\mu_1−\mu_0)}$$</block>
is the Mahalanobis distance between the populations.<br/>
The Bayes error is given by
<block class="block-center">$$\epsilon^*=(1-c)\epsilon^0[\psi^*]+c\epsilon^1[\psi^*]$$
$$=(1-c)\Phi\left(\frac{-\frac{1}{2}\delta^2+k}{\delta}\right)+c\Phi\left(\frac{-\frac{1}{2}\delta^2-k}{\delta}\right)$$</block>
In the case $P(Y=0)=P(Y=1)=\frac{1}{2}$, the previous expressions reduce to:
<block class="block-center">$$\epsilon^0[\psi^∗] = \epsilon^1[\psi^*]=\epsilon^*=\Phi\left(-\frac{\delta}{2}\right)$$</block>

### Quadratic Discriminant
Case 3: Distinct arbitrary covariance matrices.<br/>
In this case, the discriminant functions are fully quadratic
<block class="block-center">$$g_i(x)=x^TA_ix+b_i^Tx+c_i$$</block>
In the case c = 2, the single discriminant is given by:
<block class="block-center">$$g(x)=g_1(x)−g_0(x)=x^TAx+b^Tx+c = 0$$</block>
The corresponding decision surfaces are hyperquadrics, which can be exactly one of the following:
+ hyperplanes
+ pairs of parallel hyperplanes
+ pairs of intersecting hyperplanes
+ hyperspheres
+ hyperellipsoids
+ hyperparaboloids
+ hyperhyperboloids

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
