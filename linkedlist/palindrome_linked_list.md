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
    public boolean isPalindrome(ListNode head) {
        ListNode slow = head, fast = head;

        while(fast != null && fast.next!= null) {
            fast = fast.next.next;
            slow = slow.next;
        }

        if(fast != null)
            slow = slow.next;

        slow = reverse(slow);
        fast = head;

        while(slow != null) {
            if(fast.val != slow.val) {
                return false;
            }

            fast = fast.next;
            slow = slow.next;
        }

        return true;
    }

    public ListNode reverse(ListNode head) {
        ListNode rev = null;

        while(head != null) {
            ListNode temp = head.next;
            head.next = rev;
            rev = head;
            head = temp;
        }

        return rev;
    }
}
```
