## Merge Two Sorted List

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

### Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        dummy = ListNode(0)
        p = dummy
        while l1 and l2:
            if l1.val < l2.val:
                p.next = ListNode(l1.val)
                l1 = l1.next
            else:
                p.next = ListNode(l2.val)
                l2 = l2.next
            p = p.next

        if l1:
            p.next = l1
        if l2:
            p.next = l2
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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {

        ListNode dummy = new ListNode(0);
        ListNode p = dummy;

        while(l1 != null && l2 != null) {
            if(l1.val < l2.val) {
                p.next = new ListNode(l1.val);
                l1 = l1.next;
            }
            else {
                p.next = new ListNode(l2.val);
                l2 = l2.next;
            }
            p = p.next;
        }

        p.next = l1 != null ? l1 : l2;

        return dummy.next;
    }
}
```
