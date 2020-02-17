---
title: top K Frequent Elements.md
categories: leetcode
tags:
- heap
- hashmap
- priorityqueue


---

[](){:target="_blank"}

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer,Integer> map=new HashMap<>();
        
        // 10ms
        for (int num:nums) {
            map.put(num, map.getOrDefault(num,0)+1);
        }
        
        //8ms
        // int cnt=0;
        // int N=nums.length;
        // Arrays.sort(nums);
        // for (int i=0;i<N;i++) {
        //     if (i!=0 && nums[i] != nums[i-1]) {
        //         map.put(nums[i-1],cnt);
        //         cnt=1;
        //     } else {
        //         cnt++;
        //     }
        //     if (i==N-1)
        //         map.put(nums[i],cnt);
        // }
        
        PriorityQueue<Integer> q=new PriorityQueue<>((n1,n2)->(map.get(n1)-map.get(n2)));
        for (int n:map.keySet()) {
            q.add(n);
            if (q.size()>k)
                q.remove();
        }
        
        return new ArrayList(q);
    }
}
```
