---
title: Ugly Number II
categories: leetcode

---

Using DP
[https://medium.com/algorithms-and-leetcode/ugly-number-problems-on-leetcode-9375f3a34e28](https://medium.com/algorithms-and-leetcode/ugly-number-problems-on-leetcode-9375f3a34e28){:target="_blank"}

```java
class Solution {
    public int nthUglyNumber(int n) {
        int[] nums=new int[n];
        nums[0]=1;
        int num=0, n1=0,n2=0,n3=0;
        for (int i=1;i<n;i++) {
            num=Math.min(2*nums[n1], Math.min(3*nums[n2], 5*nums[n3]));
            nums[i]=num;
            if (num==nums[n1]*2) n1++;
            if (num==nums[n2]*3) n2++;
            if (num==nums[n3]*5) n3++;
        }
        return nums[n-1];
    }
    
}
```
