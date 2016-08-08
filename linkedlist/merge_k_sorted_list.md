## Merge K Sorted List

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.


### Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        heap = []
        for lh in lists:
            if lh:
                heap.append((lh.val, lh))
        heapq.heapify(heap)
        head = ListNode(0)
        cur = head
        while heap:
            h = heapq.heappop(heap)
            cur.next = ListNode(h[0])
            cur = cur.next
            if h[1].next: 
                heapq.heappush(heap, (h[1].next.val, h[1].next))
        return head.next

```