## Reverse Linked List

Reverse a singly linked list.

### Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        rev,p = None, head
        while p:
            tmp = p.next
            p.next = rev
            rev, p = p, tmp
        return rev
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
    public ListNode reverseList(ListNode head) {
        ListNode rev = null, p  = head;

        while(p != null) {
            ListNode temp = p.next;
            p.next = rev;
            rev = p;
            p = temp;
        }

        return rev;

    }
}
```
