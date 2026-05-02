---
title: Best Time to Buy and Sell Stock
tags: [array, sliding-window, easy]
---

# Best Time to Buy and Sell Stock

**Difficulty:** Easy  
**Topic:** Array, Sliding Window

---

## Problem

Given an array `prices`, find the maximum profit from buying and selling once.

## Approach

- Track minimum price seen so far
- At each step, compute profit and update max

**Time:** O(n) | **Space:** O(1)

## Solution

```java
public int maxProfit(int[] prices) {
    int minPrice = Integer.MAX_VALUE;
    int maxProfit = 0;
    for (int price : prices) {
        minPrice = Math.min(minPrice, price);
        maxProfit = Math.max(maxProfit, price - minPrice);
    }
    return maxProfit;
}
```

## Examples

| Input | Output |
|-------|--------|
| `[7,1,5,3,6,4]` | `5` |
| `[7,6,4,3,1]` | `0` |

## Edge Cases

- All decreasing prices (return 0)
- Single element array
