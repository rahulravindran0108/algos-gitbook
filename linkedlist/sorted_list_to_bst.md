## Convert Sorted List to BST

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

### Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        array = []
        p = head
        while p:
            array.append(p.val)
            p = p.next
        return self.sortedArrayToBST(array)

    def sortedArrayToBST(self, array):
        length = len(array)
        if length == 0:
            return None
        elif length == 1:
            return TreeNode(array[0])
        root = TreeNode(array[length/2])
        root.left = self.sortedArrayToBST(array[:length/2])
        root.right = self.sortedArrayToBST(array[length/2+1:])
        return root
```
