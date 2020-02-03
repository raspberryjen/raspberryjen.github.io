---
title: Merge Intervals
categories: leetcode
tags:
- Array
- Sort

---

sort->merge with queue

[https://leetcode.com/submissions/detail/299834645/](https://leetcode.com/submissions/detail/299834645/){:target="_blank"}

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        int R=intervals.length;
        if (R==0) return intervals;
        int C=intervals[0].length;
        if (C==0) return intervals;
        
        Arrays.sort(intervals, (a, b)->{return a[0]-b[0];});
        
        LinkedList<int[]> list=new LinkedList();
        for (int[] in:intervals) {
            if (list.isEmpty()) {
                list.add(in);
            } else {
                int[] last=list.getLast();
                if (last[1]<in[0])
                    list.add(in);
                else {
                    last[1]=Math.max(last[1], in[1]);
                    list.set(list.size()-1, last);
                }
            }
        }
        
        return list.toArray(new int[list.size()][C]);
    }
}
```
