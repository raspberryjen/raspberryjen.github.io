---
title: "Top K Frequent Words"
categories: leetcode

---
[https://leetcode.com/submissions/detail/294863344/](https://leetcode.com/submissions/detail/294863344/){:target="_blank"}

```
class Solution {
    //8ms/46mb
    public List<String> _topKFrequent(String[] words, int k) {
        HashMap<String, Integer> map=new HashMap<>();
        for (String word:words) {
            map.put(word,map.getOrDefault(word, 0)+1);
        }
        
        List<String> ans=new LinkedList<>(map.keySet());
        Collections.sort(ans, new Comparator<String>(){
            @Override
            public int compare(String word1, String word2) {
                int val1=map.get(word1);
                int val2=map.get(word2);
                if (val1==val2) {
                    return word1.compareTo(word2);
                } else {
                    return val2-val1;    
                }
            }
        });
        
        return ans.subList(0,k);
    }
    //6ms/46mb
    public List<String> topKFrequent(String[] words, int k) {
        HashMap<String, Integer> map=new HashMap<>();
        for (String word:words) {
            map.put(word,map.getOrDefault(word, 0)+1);
        }
        
        PriorityQueue<String> queue=new PriorityQueue<>(map.size(), (String w1, String w2)->(map.get(w1)==map.get(w2)?w1.compareTo(w2):map.get(w2)-map.get(w1))); 
        map.keySet().forEach((key)->queue.add(key));
        
        List<String> ans=new LinkedList<>();
        while (!queue.isEmpty() && ans.size()<k) {
            ans.add(queue.poll());
        }
        // System.out.println(ans);
        return ans;
    }
}
```
