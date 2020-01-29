---
title: Binary Tree Paths
categories: leetcode
tags: DFS


---

[https://leetcode.com/submissions/detail/298290501/](https://leetcode.com/submissions/detail/298290501/){:target="_blank"}

DFS
Stack & Recursive

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
    List<String> ans=new ArrayList();
    public List<String> binaryTreePaths(TreeNode root) {
        if (root==null) return ans;
        Stack<TreeNode> stack=new Stack();
        Stack<String> paths=new Stack();
        stack.add(root);
        paths.add(String.valueOf(root.val));
        
        TreeNode node=null;
        String path="";
        while(!stack.isEmpty()) {
            node=stack.pop();
            path=paths.pop();
            if (node.left==null && node.right==null)
                ans.add(path);
            if (node.left!=null) {
                stack.push(node.left);
                paths.push(path+"->"+String.valueOf(node.left.val));
            }
            if (node.right!=null) {
                stack.push(node.right);
                paths.push(path+"->"+String.valueOf(node.right.val));
            }
        }
        return ans;
        
    }
    
    public List<String> _binaryTreePaths(TreeNode root) {
        getPath("", root);
        return ans;
    }
    
    private void getPath(String path, TreeNode node) {
        if (node==null) return;
        path+=String.valueOf(node.val);
        if (node.left==null && node.right==null) ans.add(path);
        path+="->";
        if (node.left!=null) getPath(path, node.left);
        if (node.right!=null) getPath(path, node.right);
    }

}
```
