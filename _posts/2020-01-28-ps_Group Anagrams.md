---
title: Group Anagrams
categories: leetcode
tags: hash

---

[https://leetcode.com/submissions/detail/298002235/](https://leetcode.com/submissions/detail/298002235/){:target="_blank"}
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List> map=new HashMap();
        for (int i=0;i<strs.length;i++) {
            char[] chars=strs[i].toCharArray();
            Arrays.sort(chars);
            String str=String.valueOf(chars);
            List<String> list=map.getOrDefault(str, new ArrayList<String>());
            list.add(strs[i]);
            map.put(str, list);
        }
        
        return new ArrayList(map.values());
    }
}
```
