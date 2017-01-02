## Intersection of Two Linked Lists

Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:

A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.


Notes:

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.


### Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {

    public static int getListSize(ListNode head) {
        int i;
        for(i = 0;head!= null;i++)
            head = head.next;
        return i;    
    }

    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int lenA = getListSize(headA);
        int lenB = getListSize(headB);

        System.out.println(lenA + " " + lenB);
        ListNode p1 = lenA > lenB ? headA : headB;
        int diff = lenA > lenB ? lenA - lenB : lenB - lenA;

        while(diff > 0) {
            p1 = p1.next;
            diff--;
        }

        ListNode p2 = lenA > lenB ? headB : headA;

        while(p1 != null && p2 != null) {
            if(p1 == p2)
                return p1;

            p1 = p1.next;
            p2 = p2.next;
        }

        return null;
    }
}
```
