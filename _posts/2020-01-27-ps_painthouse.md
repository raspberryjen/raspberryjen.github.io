---
title: Paint House
categories: leetcode
tags:
- DP

---

Cache is important to implement DP

timi limit
```java
class Solution {
    int[][] costs;
    public int minCost(int[][] costs) {
        if (costs.length==0) return 0;
        this.costs=costs;
        return Math.min(paintCost(0,0), Math.min(paintCost(0,1), paintCost(0,2)));
    }
    private int paintCost(int n, int color) {
        int total=costs[n][color];
        if (n==costs.length-1) {
            return total;
        }
        if (color==0)
            total+=Math.min(paintCost(n+1, 1), paintCost(n+1, 2));
        else if (color==1)
            total+=Math.min(paintCost(n+1, 0), paintCost(n+1, 2));
        else if (color==2)
            total+=Math.min(paintCost(n+1, 0), paintCost(n+1, 1));
        return total;
    }
}
```

Accept
[https://leetcode.com/submissions/detail/297811966/](https://leetcode.com/submissions/detail/297811966/){:target="_blank"}

```java
class Solution {
    int[][] costs;
    Map<String, Integer> cache;
    public int minCost(int[][] costs) {
        if (costs.length==0) return 0;
        this.costs=costs;
        cache=new HashMap<>();
        return Math.min(paintCost(0,0), Math.min(paintCost(0,1), paintCost(0,2)));
    }
    private int paintCost(int n, int color) {
        if (cache.containsKey(n+"/"+color))
            return cache.get(n+"/"+color);
        
        int total=costs[n][color];
        if (n==costs.length-1) {
            return total;
        }
        if (color==0)
            total+=Math.min(paintCost(n+1, 1), paintCost(n+1, 2));
        else if (color==1)
            total+=Math.min(paintCost(n+1, 0), paintCost(n+1, 2));
        else if (color==2)
            total+=Math.min(paintCost(n+1, 0), paintCost(n+1, 1));
        cache.put(n+"/"+color, total);
        return total;
    }
}
```