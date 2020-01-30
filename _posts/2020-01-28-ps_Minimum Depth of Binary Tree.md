---
title: Minimum Depth of Binary Tree
categories: 
- leetcode
- algorithm
tags:
- DFS
- BFS
---

DFS
Recursive
[https://leetcode.com/submissions/detail/298115762/](https://leetcode.com/submissions/detail/298115762/){:target="_blank"}

```java
public int minDepth(TreeNode root) {
    if (root==null) return 0;
    if (root.left==null && root.right==null) return 1;

    int min=Integer.MAX_VALUE;
    if (root.left!=null) 
        min=Math.min(min, minDepth(root.left));
    if (root.right!=null) 
        min=Math.min(min, minDepth(root.right));

    return min+1;
}
```
using stack
```java
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null)
           return 0;
        Stack<TreeNode> stack=new Stack();
        Stack<Integer> levels=new Stack();
        stack.push(root);
        levels.push(1);
        int min=Integer.MAX_VALUE;
        while(!stack.isEmpty()) {
            TreeNode node=stack.pop();
            int level=levels.pop();
            
            if (node.left==null && node.right==null)
                min=Math.min(min, level);
            
            if (node.left!=null) {
                stack.push(node.left);
                levels.push(level+1);
            }
            if (node.right!=null) {
                stack.push(node.right);
                levels.push(level+1);
            }
        }
        return min;
    }
}
```

BFS

```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root==null) return 0;
        Queue<TreeNode> queue=new LinkedList();
        queue.add(root);
        int depth=0;
        while(!queue.isEmpty()) {
            int size=queue.size();
            for (int i=0;i<size;i++) {
                TreeNode node=queue.poll();
                if(node.left==null && node.right==null)
                    return ++depth;
                if (node.left!=null) queue.add(node.left);
                if (node.right!=null) queue.add(node.right);
            }
            depth++;
        }
        return depth;
    }
}
```


