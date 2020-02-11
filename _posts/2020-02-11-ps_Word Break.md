---
title: Word Break
categories: leetcode
tags: DP

---

DP
[https://leetcode.com/submissions/detail/302160788/](https://leetcode.com/submissions/detail/302160788/){:target="_blank"}
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> set=new HashSet(wordDict);
        boolean[] dp=new boolean[s.length()+1];
        
        dp[0]=true;
        for (int i=1;i<=s.length();i++) {
            for (int j=0;j<i;j++) {
                if (dp[j] && set.contains(s.substring(j,i))) {
                    dp[i]=true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```

Recursion with memoization
[https://leetcode.com/submissions/detail/302157829/](https://leetcode.com/submissions/detail/302157829/){:target="_blank"}

```java
class Solution {
    Boolean[] cache;
    public boolean wordBreak(String s, List<String> wordDict) {
        cache=new Boolean[s.length()];
        return wordBreak(s, new HashSet(wordDict), 0);
    }
    
    private boolean wordBreak(String s, Set<String> wordDict, int start) {
        if (start==s.length()) return true;
        
        if (cache[start]!=null) return cache[start];
        
        for (int i=start+1;i<=s.length();i++) {
            if (wordDict.contains(s.substring(start, i)) && wordBreak(s, wordDict,i))
                return cache[start]=true;
        }
        return cache[start]=false;
    }
}
```
Binary search
[https://leetcode.com/submissions/detail/302157774/](https://leetcode.com/submissions/detail/302157774/){:target="_blank"}
```java
class Solution {
    public boolean _wordBreak(String s, List<String> wordDict) {
        Set<String> wordset=new HashSet(wordDict);
        Queue<Integer> q=new LinkedList<>();
        q.add(0);
        int[] done=new int[s.length()];
        while (!q.isEmpty()) {
            int start=q.poll();
            
            if (done[start]==1) continue;
            for (int i=start+1;i<=s.length();i++) {
                if (wordset.contains(s.substring(start,i))) {
                    q.add(i);
                    if (i==s.length()) return true;
                }
            }
            done[start]=1;
        }
        return false;
    }
}
```
