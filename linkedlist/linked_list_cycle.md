## Linked List Cycle

Given a linked list, return true if cycle exists else false.

### Solution

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
         ListNode slow  = head, fast = head;

         while(fast!= null && fast.next != null) {
             fast = fast.next.next;
             slow = slow.next;

             if(slow == fast)
                return true;
         }

         return false;
    }
}
```
