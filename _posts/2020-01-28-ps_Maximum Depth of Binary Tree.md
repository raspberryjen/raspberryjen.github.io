---
title: Maximum Depth of Binary Tree
categories: leetcode
tags:
- BFS
- Recursive

---

BFS & Recursive

Recursive : [https://leetcode.com/submissions/detail/298142228/](https://leetcode.com/submissions/detail/298142228/){:target="_blank"}
BFS : [https://leetcode.com/submissions/detail/298142885/](https://leetcode.com/submissions/detail/298142885/){:target="_blank"}

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
    //BFS
    public int maxDepth(TreeNode root) {
        if (root==null) return 0;
        Stack<TreeNode> stack=new Stack();
        Stack<Integer> levels=new Stack();
        stack.add(root);
        levels.push(1);
        int max=Integer.MIN_VALUE;
        while (!stack.isEmpty()) {
            TreeNode node=stack.pop();
            int level=levels.pop();
            if (node.left==null && node.right==null)
                max=Math.max(max, level);
            if (node.left!=null) {
                stack.add(node.left);
                levels.push(level+1);
            }
            if (node.right!=null) {
                stack.add(node.right);
                levels.push(level+1);
            }
        }
        return max;
    }
    //Recursive
    public int _maxDepth(TreeNode root) {
        if (root==null) return 0;
        if (root.left==null && root.right==null) return 1;
        
        int max=Integer.MIN_VALUE;
        TreeNode node=root;
        if (node.left!=null)
            max=Math.max(max, maxDepth(node.left));
        if (node.right!=null)
            max=Math.max(max, maxDepth(node.right));
        
        return max+1;
    }
    
}
```