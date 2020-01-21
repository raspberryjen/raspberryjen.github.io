---
title: "longest palindromic substring"
categories: leetcode

---

[https://leetcode.com/submissions/detail/294578407/](https://leetcode.com/submissions/detail/294578407/){:target="_blank"}

```java
class Solution {
    public String longestPalindrome(String s) {
        if (s==null || s.length()==0) return "";
        String str="";
        String tmp="";
        for (int i=0;i<s.length();i++) {
            tmp=findPalindrome(s, i, i);
            str=(tmp.length()>str.length())?tmp:str;
            tmp=findPalindrome(s, i, i+1);
            str=(tmp.length()>str.length())?tmp:str;
        }
        return str;
    }
    
    private String findPalindrome(String s, int left, int right) {
        StringBuilder sb = new StringBuilder();
        while (left>=0 && right<s.length() && s.charAt(left)==s.charAt(right)) {
            if (left==right) {
                sb.append(s.charAt(left));
            } else {
                sb.insert(0, s.charAt(left));
                sb.append(s.charAt(right));
            }
            left--;
            right++;
        }
        return sb.toString();
    }
}
```
