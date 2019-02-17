---
title: LeetCode 121: Best Time to Buy and Sell Stock
description: Kadane's Algorithm
categories:
- Algorithm
tags:
- Algorithm
---


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
