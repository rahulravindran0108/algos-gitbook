## Find Bottom Left Tree Value

Given a binary tree, find the leftmost value in the last row of the tree.

```
Example 1:
Input:

    2
   / \
  1   3

Output:
1
```

```
Example 2:
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```

Note: You may assume the tree (i.e., the given root node) is not NULL.

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def findBottomLeftValue(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        res = [root.val, 0]
        self.dfs(root, 0, res)
        return res[0]

    def dfs(self, root, level, res):
        if root is None:
            return
        if root.left is None and root.right is None and (level == 0 or level > res[1]):
            res[0], res[1] = root.val, level

        self.dfs(root.left, level + 1, res)
        self.dfs(root.right, level + 1, res)
```
