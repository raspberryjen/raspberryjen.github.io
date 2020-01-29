---
title: Convert Sorted Array to Binary Search Tree
categories: leetcode
tags:
- DFS

---

[https://leetcode.com/articles/convert-sorted-array-to-bst/](https://leetcode.com/articles/convert-sorted-array-to-bst/){:target="_blank"}
[https://leetcode.com/submissions/detail/298345330/](https://leetcode.com/submissions/detail/298345330/){:target="_blank"}
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
    int[] nums;
    public TreeNode sortedArrayToBST(int[] nums) {
        this.nums=nums;
        return generate(0, nums.length-1);
    }
    private TreeNode generate(int left, int right) {
        if (left>right) return null;
        // choose left middle as root
        int mid=(left+right)/2;
        // choose right middle as root
        int mid=(int)Math.round((left+right)/2.0);
        TreeNode node=new TreeNode(nums[mid]);
        node.left=generate(left, mid-1);
        node.right=generate(mid+1, right);
        return node;
    }
}
```
