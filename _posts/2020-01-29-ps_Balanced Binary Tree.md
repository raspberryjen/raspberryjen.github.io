---
title: Balanced Binary Tree
categories: leetcode
tags: DFS


---

[https://leetcode.com/submissions/detail/298365545/](https://leetcode.com/submissions/detail/298365545/){:target="_blank"}

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isBalanced(TreeNode root) {
        if (root==null) return true;
        if (Math.abs(getDepth(root.left)-getDepth(root.right))>1) return false;
        return isBalanced(root.left) && isBalanced(root.right);
    }
    
    private int getDepth(TreeNode node) {
        if (node==null) return 0;
        return 1 + Math.max(getDepth(node.left), getDepth(node.right));
    }
    
}
```
