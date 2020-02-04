---
title: Subarray Sum Equals K
categories: leetcode
tags: HashMap

---

if sum[i] - sum[j] = ksum[i]−sum[j]=k, the sum of elements lying between indices ii and jj is kk.

[https://leetcode.com/submissions/detail/300035546/](https://leetcode.com/submissions/detail/300035546/){:target="_blank"}
12ms
```java
    public int subarraySum(int[] nums, int k) {
        int N=nums.length;
        int cnt=0, sum=0;
        Map<Integer, Integer> map=new HashMap();
        map.put(0, 1);
        for (int i=0;i<N;i++) {
            sum+=nums[i];
            cnt+=map.getOrDefault(sum-k, 0);
            map.put(sum, map.getOrDefault(sum, 0)+1);
        }
        return cnt;
    }
```


[https://leetcode.com/submissions/detail/300033069/](https://leetcode.com/submissions/detail/300033069/){:target="_blank"}
my solution
207ms
```java
public int subarraySum(int[] nums, int k) {
        int N=nums.length;
        if (N==0) return 0;

        int cnt=0;
        int sum=0;
        for (int i=0;i<N;i++) {
            if (nums[i]==k) {
                cnt++;
            }
            sum=nums[i];
            for (int j=i+1;j<N;j++) {
                sum+=nums[j];
                if (sum==k) {
                    cnt++;
                }
            }
        }
        return cnt;
    }
```
208ms
[https://leetcode.com/submissions/detail/300032924/](https://leetcode.com/submissions/detail/300032924/){:target="_blank"}
```java
    public int _subarraySum(int[] nums, int k) {
        int N=nums.length;
        int cnt=0;
        int sum=0;
        for (int i=0;i<N;i++) {
            sum=0;
            for (int j=i;j<N;j++) {
                sum+=nums[j];
                if (sum==k) cnt++;
            }
        }
        return cnt;
    }
```
233ms
[https://leetcode.com/submissions/detail/300032320/](https://leetcode.com/submissions/detail/300032320/){:target="_blank"}
```java
  public int __subarraySum(int[] nums, int k) {
        int N=nums.length;
        if (N==0) return 0;
        
        int cnt=0;
        int[] sum=new int[N+1];
        sum[0]=0;
        for (int i=1;i<=N;i++)
            sum[i]=sum[i-1]+nums[i-1];
        
        for (int i=0;i<N;i++) {
            for (int j=i+1;j<=N;j++) {
                if (sum[j]-sum[i]==k)
                    cnt++;
            }
        }
        return cnt;
    }
```
