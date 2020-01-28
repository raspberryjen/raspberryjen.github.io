---
title: Implement Trie (Prefix Tree)
categories: leetcode
tags: Trie


---

[https://leetcode.com/submissions/detail/298058914/](https://leetcode.com/submissions/detail/298058914/){:target="_blank"}

root link with char node
each char node can link various char node
prefix can be aggregated as same nodes

```java
class Trie {
    TrieNode root;
    /** Initialize your data structure here. */
    public Trie() {
        root=new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode node=root;
        for (char ch:word.toCharArray()) {
            if (!node.containsKey(ch))
                node.put(ch, new TrieNode());
            node=node.get(ch);
        }
        node.setEnd();
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode node=searchPrefix(word);
        return node!=null && node.isEnd();
    }
    
    private TrieNode searchPrefix(String word) {
        TrieNode node=root;
        for (char ch:word.toCharArray()) {
            if (node.containsKey(ch))
                node=node.get(ch);
            else
                return null;
        }
        return node;
        
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode node=searchPrefix(prefix);
        return node!=null;
    }
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
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
