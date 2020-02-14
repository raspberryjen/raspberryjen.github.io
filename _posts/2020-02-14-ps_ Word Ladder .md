---
title: Word Ladder 
categories: leetcode
tags:
- BFS

---

BFS solution
40ms
*ot | hot, dot, lot
h*t | hot
ho* | hot
d*t | dot
do* | dot, dog
*og | dog, log, cog
.......


[https://leetcode.com/submissions/detail/303180128/](https://leetcode.com/submissions/detail/303180128/){:target="_blank"}

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        int L=beginWord.length();
        Map<String, List<String>> map=new HashMap<>();
        wordList.forEach(
            word->{
                for (int i=0;i<L;i++) {
                    String sub=word.substring(0,i)+'*'+word.substring(i+1,L);
                    List<String> list=map.getOrDefault(sub, new ArrayList<>());
                    list.add(word);
                    map.put(sub,list);
                }
            }
        );
        
        Queue<Pair<String,Integer>> q=new LinkedList<>();
        q.add(new Pair(beginWord,1));
        
        Map<String, Boolean> visited=new HashMap<>();
        visited.put(beginWord,true);
        
        while (!q.isEmpty()) {
            Pair<String, Integer> node=q.poll();
            String word=node.getKey();
            int level=node.getValue();
            for (int i=0;i<L;i++) {
                String sub=word.substring(0,i)+'*'+word.substring(i+1,L);
                for (String str:map.getOrDefault(sub,new ArrayList<>())) {
                    if (str.equals(endWord)) {
                        return level+1;
                    }
                    if (!visited.containsKey(str)) {
                        visited.put(str,true);
                        q.add(new Pair(str,level+1));
                    }
                }
            }
        }
        return 0;
    }
}
```


my solution
592ms
[https://leetcode.com/submissions/detail/303102799/](https://leetcode.com/submissions/detail/303102799/){:target="_blank"}

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        if (beginWord.isEmpty() || !wordList.contains(endWord)) return 0;
        
        int depth=0;
        int N=wordList.size();
        int[] done=new int[N];
        Queue<String> q=new LinkedList<>();
        q.add(beginWord);
        while(!q.isEmpty()) {
            int size=q.size();
            for (int i=0;i<size;i++) {
                String str=q.poll();
                if (str.equals(endWord)) return depth+1;
                for (int j=0;j<N;j++) {
                    if (done[j]==1) continue;
                    String word=wordList.get(j);
                    if (matchCnt(str,word)==str.length()-1) {
                        q.add(word);
                        done[j]=1;
                    }
                }
            }
            depth++;
        }
        return 0;
    }
    
    private int matchCnt(String str, String word) {
        int match=0;
        for (int i=0;i<word.length();i++) {
            if (word.charAt(i)==str.charAt(i))
                match++;
        }
        return match;
    }
}
```

discussion solution
55ms
match function logic is different
```java
// core logic: classic BFS: starting from the begin word, do a BFS till you encounter the end word. if you don't find end word by the end of the process, return 0
    // level 1: hit  level 2: hot  level 3: dot, lot   level 4: dog, log   level 5: cog  (this is for example 1)
    // TC: O(m * n) -> where m is the length of word list and n is the length of each word
    private static int ladderLength(String beginWord, String endWord, List<String> wordList) {
        if (!wordList.contains(endWord)) {
            return 0;
        }

        int level = 0;
        Queue<String> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>(wordList);
        queue.offer(beginWord);

        while (!queue.isEmpty()) {
            int queueSize = queue.size();
            for (int i = 0; i < queueSize; i++) {
                String word = queue.poll();
                if (word.equals(endWord)) {
                    return level + 1;
                }
                wordMatch(queue, visited, word);
            }
            level++;
        }
        return 0;
    }

    // helper method to transform all the letters of the given word and generate the possibilities of new words (eg: hit will be matched to hot and hot will be matched to dot and lot from the first example). only one letter will be replaced from the given word to generate all the possibilities.
    private static void wordMatch(Queue<String> queue, Set<String> visited, String word) {
        for (int i = 0; i < word.length(); i++) {
            char[] wordArray = word.toCharArray();
            for (char ch = 'a'; ch < 'z'; ch++) {
                wordArray[i] = ch;

                String newWord = String.valueOf(wordArray);
                if (visited.contains(newWord)) {
                    visited.remove(newWord);
                    queue.offer(newWord);
                }
            }
        }
    }
```