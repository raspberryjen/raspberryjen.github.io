---
title: Boundary of Binary Tree
categories: leetcode
tags: Tree

---

[https://leetcode.com/submissions/detail/305072035/](https://leetcode.com/submissions/detail/305072035/){:target="_blank"}

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
    List<Integer> ans=new ArrayList<>();
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        if (root==null) return ans;
        
        ans.add(root.val);
        
        left(root.left);
        leaves(root.left);
        leaves(root.right);
        right(root.right);
        return ans;
    }
    
    private void left(TreeNode node) {
        if (node==null || (node.left==null && node.right==null)) return;
        ans.add(node.val);
        if (node.left!=null)
            left(node.left);
        else
            left(node.right);
    }
    
    private void leaves(TreeNode node) {
        if (node==null) return;
        if (node.left==null && node.right==null)
            ans.add(node.val);
        else {
            leaves(node.left);
            leaves(node.right);
        }
    }
    
    private void right(TreeNode node) {
        if (node==null || (node.left==null && node.right==null)) return;
        if (node.right!=null)
            right(node.right);
        else
            right(node.left);
        ans.add(node.val);
    }
    
}
```
