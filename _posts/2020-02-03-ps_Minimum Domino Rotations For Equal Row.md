---
title: Minimum Domino Rotations For Equal Row
categories: leetcode
tags: Greedy

---



[https://leetcode.com/submissions/detail/299784114/](https://leetcode.com/submissions/detail/299784114/){:target="_blank"}

```java
class Solution {
    private int check(int x, int[] A, int[] B) {
        int cnt_a=0,cnt_b=0;
        for (int i=0;i<A.length;i++) {
            int a=A[i];
            int b=B[i];
            if (a!=x && b!=x) return -1;
            else if (a!=x) cnt_a++;
            else if (b!=x) cnt_b++;
        }
        return Math.min(cnt_a, cnt_b);
    }
    
    public int minDominoRotations(int[] A, int[] B) {
        int cnt=check(A[0], A, B);
        if (cnt!=-1) return cnt;
        return check(B[0], A, B);
    }
}
```
