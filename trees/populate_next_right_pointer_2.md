## Populate Next Right Pointer 2

Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

### Solution

```python
# Definition for binary tree with next pointer.
# class TreeLinkNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
#         self.next = None

class Solution(object):
    def connect(self, root):
        """
        :type root: TreeLinkNode
        :rtype: nothing
        """
        current = root
        while current:
            next, prev = None, None
            while current:
                if next is None:
                    next = current.left if current.left else current.right
                if current.left:
                    if prev: prev.next = current.left
                    prev = current.left
                if current.right:
                    if prev: prev.next = current.right
                    prev = current.right
                current = current.next
            current = next
```
