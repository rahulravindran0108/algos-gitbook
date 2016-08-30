## Convert Sorted Array to Binary Tree

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        return self.createBST(nums, 0, len(nums) - 1)

    def createBST(self, nums, start, end):
        if start > end:
            return None
        mid = (start + end) / 2
        root = TreeNode(nums[mid])
        root.left = self.createBST(nums, start, mid - 1)
        root.right = self.createBST(nums, mid + 1, end)
        return root
```
