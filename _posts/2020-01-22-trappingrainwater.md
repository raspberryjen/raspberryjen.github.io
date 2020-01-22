---
title:Trapping Rain Water
categories:leetcode

---

[https://leetcode.com/submissions/detail/296313531/](https://leetcode.com/submissions/detail/296313531/){:target="_blank"}

```java
class Solution {
    private int getHigest(int[] height) {
        int max=0;
        for (int n:height)
            max=Math.max(max, n);
        return max;
    }
    // 87ms
    public int _trap(int[] height) {
        int N=height.length;
        int water=0;
        for (int i=0;i<N;i++) {
            int left=getHigest(Arrays.copyOfRange(height, 0, i));
            int right=getHigest(Arrays.copyOfRange(height, i+1,N));
            int amount=Math.min(left,right)-height[i];
            if (amount >0)
                water+=amount;
        }
        return water;
    }
    // 32ms
    public int __trap(int[] height) {
        if (height==null || height.length==0) return 0;
        int N=height.length;
        int[] left_max=new int[N];
        left_max[0]=height[0];
        for (int i=1;i<N;i++) {
            left_max[i]=Math.max(height[i], left_max[i-1]);
        }
        
        int[] right_max=new int[N];
        right_max[N-1]=height[N-1];
        for (int i=N-2;i>=0;i--) {
            right_max[i]=Math.max(height[i], right_max[i+1]);
        }
        int water=0, val=0;
        for (int i=1;i<N-1;i++) {
            System.out.println(i);
            val=Math.min(left_max[i], right_max[i])-height[i];
            if (val>0)
                water+=val;
        }
        return water;
    }
    
    public int trap(int[] height) {
        if (height==null || height.length==0) return 0;
        int N=height.length;
        int left=0, right=N-1;
        int left_max=0,right_max=0;
        int water=0;
        while (left<right) {
            if (height[left]<=height[right]) {
                if (height[left]>left_max) {
                    left_max=height[left];
                } else {
                    water+=left_max-height[left];
                }
                left++;
            } else {
                if (height[right]>right_max) {
                    right_max=height[right];
                } else {
                    water+=right_max-height[right];
                }
                right--;
            }
            
        }
        return water;
    }
}
```
