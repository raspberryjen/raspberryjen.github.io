---
title: Min Cost Climbing Stairs
categories: leetcode
tags:
- fibonacci

---

[https://leetcode.com/submissions/detail/297512376/](https://leetcode.com/submissions/detail/297512376/){:target="_blank"}

come from (i - 2)-th stair or (i - 1)-th stair.
current cost + min(i-1 total cost, i-2 total cost)

```java
    public int minCostClimbingStairs(int[] cost) {
        int[] cache=new int[cost.length];
        cache[0]=cost[0];
        cache[1]=cost[1];
        for (int i=2;i<cost.length;i++) {
            cache[i]=cost[i] + Math.min(cache[i-1], cache[i-2]);
        }
        return Math.min(cache[cost.length-1], cache[cost.length-2]);
    }
```