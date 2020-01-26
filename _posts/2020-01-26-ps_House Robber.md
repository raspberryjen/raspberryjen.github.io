---
title: House Robber
categories: leetcode
tags:
- DP

---

compare between previous max and current max value

[https://leetcode.com/submissions/detail/297547789/](https://leetcode.com/submissions/detail/297547789/){:target="_blank"}

```java
    public int rob(int[] nums) {
        if (nums==null || nums.length==0) return 0;
        if (nums.length==1) return nums[0];
        if (nums.length==2) return Math.max(nums[0], nums[1]);
        int[] cache=new int[nums.length];
        cache[0]=nums[0];
        cache[1]=Math.max(cache[0], nums[1]);
        for (int i=2;i<nums.length;i++) {
            cache[i]=Math.max(cache[i-2]+nums[i],cache[i-1]);
        }
        return cache[nums.length-1];
    }
```