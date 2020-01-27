---
title: Palindrome Linked List
categories: leetcode
tags:
- two pinters


---

[](){:target="_blank"}

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
    ListNode orgHead;
    private boolean check(ListNode node) {
        if (node==null) return true;
        if (!check(node.next)) return false;
        if (orgHead.val!=node.val) return false;
        orgHead=orgHead.next;
        return true;
    }
    //1ms
    public boolean isPalindrome(ListNode head) {
        this.orgHead=head;
        return check(head);
    }
    //3ms
    public boolean _isPalindrome(ListNode head) {
        List<Integer> list=new ArrayList<>();
        while (head!=null) {
            list.add(head.val);
            head=head.next;
        }
        int left=0,right=list.size()-1;
        while(left<right) {
            if ((int)list.get(left)!=(int)list.get(right)) return false;
            left++;
            right--;
        }
        return true;
    }
}
```

Advanced solution : no extra memory
```java
class Solution {

    public boolean isPalindrome(ListNode head) {

        if (head == null) return true;

        // Find the end of first half and reverse second half.
        ListNode firstHalfEnd = endOfFirstHalf(head);
        ListNode secondHalfStart = reverseList(firstHalfEnd.next);

        // Check whether or not there is a palindrome.
        ListNode p1 = head;
        ListNode p2 = secondHalfStart;
        boolean result = true;
        while (result && p2 != null) {
            if (p1.val != p2.val) result = false;
            p1 = p1.next;
            p2 = p2.next;
        }        

        // Restore the list and return the result.
        firstHalfEnd.next = reverseList(secondHalfStart);
        return result;
    }

    // Taken from https://leetcode.com/problems/reverse-linked-list/solution/
    private ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode nextTemp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextTemp;
        }
        return prev;
    }

    private ListNode endOfFirstHalf(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
}
```