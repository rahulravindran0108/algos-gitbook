## Recover Binary Search Tree

Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

Note:
A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

## Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def recoverTree(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        self.n1 = self.n2 = self.prev = None
        self.findNodes(root)
        self.n1.val, self.n2.val = self.n2.val, self.n1.val

    def findNodes(self, root):
        if root:
            self.findNodes(root.left)
            if self.prev and self.prev.val > root.val:
                self.n2 = root
                if self.n1 == None: self.n1 = self.prev
            self.prev = root
            self.findNodes(root.right)
```
