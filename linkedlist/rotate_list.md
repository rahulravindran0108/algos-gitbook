## Rotate List

Given a list, rotate the list to the right by k places, where k is non-negative.
```
For example:
Given 1->2->3->4->5->NULL and k = 2,
return 4->5->1->2->3->NULL.
```

### Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if(head == null || head.next == null)
            return head;
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode slow = dummy, fast = dummy;

        int i;

        for(i = 0; fast.next != null;i++)
            fast = fast.next;

        for(int j = i - k % i; j > 0;j --)
            slow = slow.next;

        fast.next = dummy.next;
        dummy.next = slow.next;
        slow.next = null;

        return dummy.next;
    }
}
```
