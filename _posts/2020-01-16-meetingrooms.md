---
title: "meeting rooms 2"
categories: leetcode

---
[https://leetcode.com/submissions/detail/294700454/](https://leetcode.com/submissions/detail/294700454/){:target="_blank"}

```
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        if (intervals == null || intervals.length == 0) {
            return 0;
        }
        
        // sort asceding with start time
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
        
        // queuing with end time
        PriorityQueue<Integer> allocator = new PriorityQueue<>();
        allocator.add(intervals[0][1]);
        for (int i = 1; i < intervals.length; i++) {
            // start time >= allocated sche
            // if already done, remove
            if (intervals[i][0] >= allocator.peek()) {
                allocator.poll();
            }
            //add next one
            allocator.add(intervals[i][1]);
        }
        return allocator.size();
    }
    
}
```
