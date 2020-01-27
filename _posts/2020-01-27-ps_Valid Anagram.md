---
title: Valid Anagram
categories: leetcode
tags: 
- sort

---


[https://leetcode.com/submissions/detail/297845508/](https://leetcode.com/submissions/detail/297845508/){:target="_blank"}

```java
class Solution {
    // 3 ms
    public boolean isAnagram(String s, String t) {
        if (s.equals(t)) return true;
        if (s.length()!=t.length()) return false;
        
        int[] counter=new int[26];
        for (int i=0;i<s.length();i++) {
            counter[s.charAt(i)-'a']++;
            counter[t.charAt(i)-'a']--;
        }
        for (int count:counter) {
            if (count!=0)
                return false;
        }
        return true;
    } 
    // 3 ms
    public boolean __isAnagram(String s, String t) {
        if (s.equals(t)) return true;
        if (s.length()!=t.length()) return false;
        
        char[] schars=s.toCharArray();
        char[] tchars=t.toCharArray();
        Arrays.sort(schars);
        Arrays.sort(tchars);
        return Arrays.equals(schars,tchars);
        
    }
    // 15 ms
    public boolean _isAnagram(String s, String t) {
        if (s.equals(t)) return true;
        if (s.length()!=t.length()) return false;
        
        HashMap<Character, Integer> map=new HashMap<>();
        for (char c:s.toCharArray()) {
            map.put(c,map.getOrDefault(c,0)+1);
        }
        for (char c:t.toCharArray()) {
            map.put(c,map.getOrDefault(c,0)-1);
        }
        for (char c:map.keySet()) {
            if (map.get(c)!=0) return false;
        }
        return true;
    }
}
```