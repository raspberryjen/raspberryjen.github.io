---
title: "Longest Substring Without Repeating Characters"
date: 2020-01-16 11:48:28 +0900
categories: leetcode

---

172ms : [https://leetcode.com/submissions/detail/294606360/](https://leetcode.com/submissions/detail/294606360/){:target="_blank"}

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s.isEmpty()) return 0;
        if (s.length()==1) return 1;
        
        int max=0, cnt=0;
        String res="";
        for (int i=0;i<s.length()-1;i++) {
            res=s.substring(i, i+1);
            cnt=1;
            for (int j=i+1;j<s.length();j++) {
                if (res.contains(s.substring(j,j+1))) break;
                else {
                    res += s.substring(j, j+1);
                    cnt++;
                    // System.out.println(res);
                }
            }
            max=Math.max(max, cnt);
        }
        return max;
    }
}
```

11ms : [https://leetcode.com/submissions/detail/294636963/](https://leetcode.com/submissions/detail/294636963/){:target="_blank"}
```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n=s.length();
        Set<Character> set=new HashSet<>();
        int max=0;
        int i=0,j=0;
        while(i<n&&j<n) {
            if (set.contains(s.charAt(j))) {
                set.remove(s.charAt(i++));
            } else {
                set.add(s.charAt(j++));
                max=Math.max(max, j-i);
            }
        }
        return max;
    }
    
}
```
