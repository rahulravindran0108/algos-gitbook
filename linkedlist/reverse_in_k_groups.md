## Reverse Nodes in K Groups

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

You may not alter the values in the nodes, only nodes itself may be changed.

Only constant memory is allowed.

For example,
Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5

### Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverse(self, start, end):
        p = ListNode(0)
        p.next = start
        while p.next != end:
            tmp = start.next
            start.next = tmp.next
            tmp.next = p.next
            p.next = tmp
        return [end, start]

    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if head is None:
            return None
        dummy = ListNode(0)
        dummy.next, p = head, dummy
        while p.next:
            end = p
            for i in range(k-1):
                end = end.next
                if end.next is None:
                    return dummy.next
            res = self.reverse(p.next, end.next)
            p.next=res[0]
            p=res[1]
        return dummy.next

```
