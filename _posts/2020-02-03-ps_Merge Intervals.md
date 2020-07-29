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

50ms
[https://leetcode.com/submissions/detail/373095546/](https://leetcode.com/submissions/detail/373095546/){:target="_blank"}
'''java
public int[][] merge(int[][] intervals) {
 if (intervals.length <= 1)
        return intervals;
    int[][] ans = new int[][] {};
    List<int[]> list = new LinkedList<>(Arrays.asList(intervals));
    list.sort((e1, e2) -> e1[0] - e2[0]);
    // dump(list);
    List<int[]> ansl = new LinkedList<>();
    ansl.add(list.get(0));

    int i=1;
    while (i<list.size()) {
        int[] c = list.get(i);
        int idx=ansl.size()-1;
        int[] p = ansl.get(idx);
        if (c[0] > p[1]) {
            ansl.add(c);
        } else if (c[0] <= p[1] && p[1] < c[1]) {
            p[1] = c[1];
        }
        i++;
    }
    // dump(ansl);
    ans = ansl.toArray(ans);
    return ans;
}
'''
