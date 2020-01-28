---
title: Minimum Depth of Binary Tree
categories: leetcode
tags:
- DFS

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
        if (root==null) return 0;
        Stack<TreeNode> stack=new Stack();
        int min=Integer.MAX_VALUE;
        TreeNode node=root, prev=null;
        while(node!=null || !stack.isEmpty()) {
            if (node!=null) {
                stack.push(node);
                node=node.left;
            } else {
                TreeNode pn=stack.peek();
                if (pn.right!=null && pn.right != prev) {
                    node=pn.right;
                } else {
                    if (pn.left==null && pn.right==null)
                        min=Math.min(min, stack.size());
                    prev=stack.pop();
                }
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


