---
title: Climbing Stairs
categories: leetcode
tags:
- fibonacci

---

[https://youtu.be/d0oiDbuSr-I](https://youtu.be/d0oiDbuSr-I){:target="_blank"}

n=1 : 1
n=2 : 11    2
n=3 : 111   21  12
n=4 : 1111  211 112 122 22
n=5 : 1111  2111 1121 1221 221 1112 212 122
n   : (n-1 + 1 step) + (n-2 + 2 steps)



time limit (O(2^n))
```java
    public int climbStairs(int n) {
        if (n<2) return 1;
        return climbStairs(n-1) + climbStairs(n-2);
    }

```
Accept
```java
    public int climbStairs(int n) {
        if (n<2) return 1;
        int[] cache=new int[n+1];
        cache[0]=1;
        cache[1]=1;
        for (int i=2;i<n+1;i++) {
            cache[i]=cache[i-1]+cache[i-2];
        }
        return cache[n];
    }
```

