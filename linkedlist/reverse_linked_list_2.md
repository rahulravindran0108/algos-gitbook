## Reverse Linked List 2

Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.

Note:
Given m, n satisfy the following condition:
1 ≤ m ≤ n ≤ length of list.

### Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        if head is None or head.next is None:
            return head
        dummy = ListNode(0)
        dummy.next = head
        p1 = dummy
        for i in xrange(m - 1):
            p1 = p1.next
        p = p1.next
        for i in xrange(n - m):
            tmp = p1.next
            p1.next = p.next
            p.next = p.next.next
            p1.next.next = tmp
        return dummy.next
```

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
    public ListNode reverseBetween(ListNode head, int m, int n) {
        if(head == null)
            return null;

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;

        for(int i=0;i< m - 1;i++)
            pre = pre.next;

        ListNode start = pre.next;
        ListNode then = start.next;

        for(int i = 0;i< n - m;i++) {
            start.next = then.next;
            then.next = pre.next;
            pre.next = then;
            then = start.next;
        }

        return dummy.next;
    }
}
```
