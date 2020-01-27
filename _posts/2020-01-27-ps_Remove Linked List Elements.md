---
title: Remove Linked List Elements
categories: leetcode
tags:
- Linked List

---

[https://leetcode.com/submissions/detail/297851125/](https://leetcode.com/submissions/detail/297851125/){:target="_blank"}


```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    //2ms
    public ListNode _removeElements(ListNode head, int val) {
        if (head==null) return null;
        if (head.val==val) {
            return removeElements(head.next,val);      
        } else {
            head.next=removeElements(head.next,val);
            return head;
        }
    }
}
```