---
title: Remove Element
categories: leetcode
tags:
- two pointers
- array

---

[https://leetcode.com/submissions/detail/297861961/](https://leetcode.com/submissions/detail/297861961/){:target="_blank"}

```java
class Solution {
    //0ms
    public int removeElement(int[] nums, int val) {
        int idx=0;
        for (int i=0;i<nums.length;i++) {
            if (nums[i]!=val) {
                nums[idx++]=nums[i];
            }
        }
        return idx;
    }
    //1ms
    public int _removeElement(int[] nums, int val) {
        Arrays.sort(nums);
        int s=-1,e=-1;
        int cnt=0;
        for (int i=0;i<nums.length;i++) {
            if (nums[i]==val) {
                if (s==-1) s=i;
                cnt++;
            }
            if (s!=-1 && (nums[i]>val || i==nums.length-1)) {
                if (e==-1) e=i;
                break;
            }
        }
        if (s==-1) return nums.length;
        for (int i=s,j=e;i<nums.length;i++,j++) {
            if (j>=nums.length) break;
            nums[i]=nums[j];
        }
        return nums.length-cnt;
    }
}
```