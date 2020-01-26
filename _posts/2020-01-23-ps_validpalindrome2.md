---
title: Valid Palindrome II
categories: leetcode

---

[https://leetcode.com/submissions/detail/297246076/](https://leetcode.com/submissions/detail/297246076/){:target="_blank"}
```java
class Solution {
    private boolean isPalindrome(String s) {
        int left=0,right=s.length()-1;
        while (left<right) {
            if (s.charAt(left)!=s.charAt(right))
                return false;
            left++;
            right--;
        }
        return true;
    }
    public boolean validPalindrome(String s) {
        if (s.isEmpty()) return false;
        if (s.length()==1) return true;
        
        int left=0,right=s.length()-1;
        while (left<right) {
            if (s.charAt(left)!=s.charAt(right)) {
                return isPalindrome(s.substring(left,right)) || isPalindrome(s.substring(left+1,right+1));
            } else {
                left++;
                right--;
            }
        }
        return true;
    }
}
```
