## Palindrome Linked List

Given a singly linked list, determine if it is a palindrome.

Follow up:
Could you do it in O(n) time and O(1) space?

### Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if head is None:
          return None
        slow = fast = head
        while fast.next and fast.next.next:
          slow = slow.next
          fast = fast.next.next
        p, last = slow.next, None
        while p:
          next = p.next
          p.next = last
          last, p = p, next
        p1, p2 = last, head
        while p1.val and p1.val == p2.val:
          p1, p2 = p1.next, p2.next
        return p1 is None
```
