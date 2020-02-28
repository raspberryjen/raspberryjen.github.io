---
title: Search Suggestions System
categories: leetcode
tags:


---

make pool with previous list
the latest suggestions should be subset in previous list

12ms
[https://leetcode.com/submissions/detail/305315694/](https://leetcode.com/submissions/detail/305315694/){:target="_blank"}

```java
class Solution {
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {
        List<List<String>> ans= new ArrayList<>();
        int N=searchWord.length();
        if (N==0) return ans;
        
        Arrays.sort(products);
        List<String> pool=Arrays.asList(products);
        for (int i=1;i<=N;i++) {
            String str=searchWord.substring(0,i);
            List<String> words=new ArrayList<>();
            pool.forEach(word->{if (word.startsWith(str)) words.add(word);});
            int e = (words.size()<3) ? words.size():3;
            ans.add(words.subList(0,e));
            pool=words;
        }
        return ans;
    }
}
```

my solution : 27ms
[https://leetcode.com/submissions/detail/305295456/](https://leetcode.com/submissions/detail/305295456/)
```java
class Solution {
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {
        List<List<String>> ans= new ArrayList<>();
        if (searchWord.isEmpty()) return ans;
        
        Arrays.sort(products);
        for (int i=1;i<=searchWord.length();i++) {
            String str=searchWord.substring(0,i);
            List<String> words=new ArrayList<>();
            for (String word:products) {
                if (words.size()==3) break;
                if (word.startsWith(str))
                    words.add(word);
            }
            ans.add(words);
        }
        return ans;
    }
}
```