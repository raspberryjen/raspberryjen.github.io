---
title: "add-two-numbers"
date: 2020-01-15 08:26:28 +0900
categories: leetcode

---

[https://leetcode.com/submissions/detail/294267411/](https://leetcode.com/submissions/detail/294267411/){:target="_blank"}

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
    private ListNode addTwo(ListNode l1, ListNode l2, int carry) {
        if (l1==null && l2==null && carry==0) return null;
        int sum=((l1!=null)?l1.val:0) + ((l2!=null)?l2.val:0) + carry;
        int val=(sum)%10;
        ListNode node=new ListNode(val);
        if (l1!=null || l2!=null || (sum/10)>=1)
            node.next=addTwo((l1!=null)? l1.next:null, (l2!=null)?l2.next:null, sum/10);
        return node;
    }

    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        return addTwo(l1, l2, 0);
    }
}
```
