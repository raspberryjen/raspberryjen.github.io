---
title: Next Permutation
categories: leetcode
tags: Array


---

next permutation(다음 순열) 예측 in lexicographically(사전적) order
불가한 경우 오름차순으로 정렬


Solution

[https://leetcode.com/submissions/detail/302941986/](https://leetcode.com/submissions/detail/302941986/){:target="_blank"}
```java
class Solution {
    public void nextPermutation(int[] nums) {
        int i=nums.length-2;
        while (i>=0 && nums[i]>=nums[i+1]) {
            i--;
        }
        if (i>=0) {
            int j=nums.length-1;
            while (j>=0 && nums[j]<=nums[i]) {
                j--;
            }
            swap(nums,i,j);
        }
        reverse(nums, i+1);
    }
    
    private void swap(int[] nums, int i, int j) {
        int tmp=nums[i];
        nums[i]=nums[j];
        nums[j]=tmp;
    }
    
    // using quick sort
    private void reverse(int[] nums, int s) {
        int i=s,j=nums.length-1;
        while(i<j) {
            swap(nums,i,j);
            i++;
            j--;
        }
    }
}
```


my solution
[https://leetcode.com/submissions/detail/302910836/](https://leetcode.com/submissions/detail/302910836/){:target="_blank"}

```java
class Solution {
    public void nextPermutation(int[] nums) {
        if (nums.length<=1) return;
        if (nums.length==2 && nums[0]<nums[1]) {
            int tmp=nums[0];
            nums[0]=nums[1];
            nums[1]=tmp;
            return;
        }
        
        int min=Integer.MAX_VALUE;
        int minIdx=-1;
        int i=nums.length-2;
        for (;i>=0;i--) {
            for (int j=i+1;j<nums.length;j++) {
                if (nums[j]>nums[i] && nums[j]<min) {
                    min=nums[j];
                    minIdx=j;
                }
            }
            if (minIdx!=-1) break;
        }
        if (minIdx!=-1) {
            nums[minIdx]=nums[i];
            nums[i]=min;
            int[] sub=Arrays.copyOfRange(nums, i+1,nums.length);
            Arrays.sort(sub);
            int idx=0;
            for (int j=i+1;j<nums.length;j++) {
                nums[j]=sub[idx++];
            }
        } else {
            Arrays.sort(nums);
        }
    }
}
```