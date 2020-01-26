---
title: Fibonacci Number
categories: leetcode
tags: fibonacci

---

Fibonacci sequence
```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), for N > 1.
```

[](){:target="_blank"}


Recursion
: Time complexity : O(2^N)

```java
    public int fib(int N) {
        if (N<=1) return N;
        return fib(N-1)+fib(N-2);
    }
```

Bottom-Up Approach using Memoization
: O(N)
```java
    public int fib(int N) {
        if (N<=1) return N;
        return fib(N-1)+fib(N-2);
    }
    
    private int doCache(int N) {
        int[] cache=new int[N+1];
        cache[1]=1;
        
        for (i=2;i<N+1;i++) {
            cache[i]=cache[i-1]+cache[i-2];
        }
        return cache[N];
    }
```

