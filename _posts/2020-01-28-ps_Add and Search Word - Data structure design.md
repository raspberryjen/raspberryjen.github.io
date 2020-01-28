---
title: Add and Search Word - Data structure design
categories: leetcode
tags:
- Trie

---

search recursively with increased word position
```
if (ch=='.') {
    for (TrieNode n:node.getLinks())
        if (search(word, pos+1, n)) return true;
} else {
    return search(word, pos+1, node.get(ch));
}
```        

[https://leetcode.com/submissions/detail/298090799/](https://leetcode.com/submissions/detail/298090799/){:target="_blank"}

```java
class WordDictionary {
    TrieNode root;
    /** Initialize your data structure here. */
    public WordDictionary() {
        root=new TrieNode();
    }
    
    /** Adds a word into the data structure. */
    public void addWord(String word) {
        TrieNode node=root;
        for (char ch:word.toCharArray()) {
            if (!node.containsKey(ch))
                node.put(ch, new TrieNode());
            node=node.get(ch);
        }
        node.setEnd();
    }
    
    private boolean search(String word, int pos, TrieNode node) {
        if (node==null) return false;
        if (pos==word.length()) return node.isEnd();
        char ch=word.charAt(pos);
        if (ch=='.') {
            for (TrieNode n:node.getLinks())
                if (search(word, pos+1, n)) return true;
        } else {
            return search(word, pos+1, node.get(ch));
        }
        return false;
    }
    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean search(String word) {
        return search(word, 0, root);
    }
    
    class TrieNode {
        // 26 links to node children
        private TrieNode[] links;
        private boolean isEnd;

        public TrieNode() {
            links = new TrieNode[26];
        }

        public boolean containsKey(char ch) {
            return links[ch -'a'] != null;
        }
        public TrieNode get(char ch) {
            return links[ch -'a'];
        }
        public void put(char ch, TrieNode node) {
            links[ch -'a'] = node;
        }
        public void setEnd() {
            isEnd = true;
        }
        public boolean isEnd() {
            return isEnd;
        }
        public TrieNode[] getLinks() {
            return links;
        }
    }
}

/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```
