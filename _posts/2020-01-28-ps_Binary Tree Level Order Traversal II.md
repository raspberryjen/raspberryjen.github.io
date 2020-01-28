---
title: Binary Tree Level Order Traversal II
categories: leetcode
tags: BFS


---

recursive
[https://leetcode.com/submissions/detail/298109891/](https://leetcode.com/submissions/detail/298109891/){:target="_blank"}
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
    List<List<Integer>> ans;
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        if (root==null) return new ArrayList();
        ans=new ArrayList();
        ans.add(0, new ArrayList(Arrays.asList(root.val)));

        generate(1, root.left);
        generate(1, root.right);
        
        Collections.reverse(ans);
        return ans;
    }
    
    private void generate(int level, TreeNode node) {
        if (node==null) return;
        
        List<Integer> list=null;
        if (level>=ans.size()) {
            ans.add(level, new ArrayList(Arrays.asList(node.val)));
        } else {
            list=ans.get(level);
            list.add(node.val);
            ans.set(level, list);
        }
        
        if (node.left!=null)
            generate(level+1, node.left);
        if (node.right!=null)
            generate(level+1, node.right);
    }
}
```

using queue
[https://leetcode.com/submissions/detail/298113231/](https://leetcode.com/submissions/detail/298113231/){:target="_blank"}
```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> ans=new ArrayList();
        if (root==null) return ans;
        Queue<TreeNode> queue=new LinkedList();
        queue.add(root);
        while(!queue.isEmpty()) {
            List<Integer> list=new ArrayList();
            int size=queue.size();
            for (int i=0;i<size;i++) {
                TreeNode node=queue.poll();
                list.add(node.val);
                if (node.left!=null) queue.add(node.left);
                if (node.right!=null) queue.add(node.right);
            }
            if (!list.isEmpty()) ans.add(list);
        }       
        Collections.reverse(ans);
        return ans;        
        
    }
}
```
