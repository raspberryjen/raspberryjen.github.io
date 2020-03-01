---
title: Minimum Cost to Connect Sticks
categories: leetcode
tags:
- greedy
- PriorityQueue

---

[https://leetcode.com/submissions/detail/308172266/](https://leetcode.com/submissions/detail/308172266/){:target="_blank"}


```java
class Solution {
    public int connectSticks(int[] sticks) {
        if (sticks.length<2) return 0;
        
        PriorityQueue<Integer> q=new PriorityQueue<>();
        for (int stick:sticks) {
            q.add(stick);
        }
        int sum=0;
        while (q.size()>1) {
            int val=q.poll()+q.poll();
            sum+=val;
            q.add(val);
        }
        return sum;
    }
}
```
