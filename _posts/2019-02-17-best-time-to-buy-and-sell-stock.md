---
title: LeetCode 121. Best Time to Buy and Sell Stock
description: Kadane's Algorithm
categories:
- Algorithm
tags:
- Algorithm
---


![profit](/assets/images/post/best-time-to-buy-and-sell-stock/profit.png)
## Question:
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.
<!-- more -->

## Solution:
### Kadane's Algorithm
```java
public int maxProfit(int[] prices) {
    int maxCur = 0, maxSoFar = 0;
    for(int i = 1; i < prices.length; i++) {
        maxCur = Math.max(0, maxCur += prices[i] - prices[i - 1]);
        maxSoFar = Math.max(maxCur, maxSoFar);
    }
    return maxSoFar;
}
```
