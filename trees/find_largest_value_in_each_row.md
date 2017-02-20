## Find Largest Value in Each row

You need to find the largest value in each row of a binary tree.

```
Example:
Input:

          1
         / \
        3   2
       / \   \  
      5   3   9

Output: [1, 3, 9]
```

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
import sys
from collections import defaultdict

class Solution(object):
    def largestValues(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        res = defaultdict(lambda: -sys.maxint)

        self.dfs(res, root, 0)
        return [res[key] for key in sorted(res)]

    def dfs(self, res, root, level):
        if root is None:
            return
        res[level] = max(res[level],root.val)
        self.dfs(res, root.left, level + 1)
        self.dfs(res, root.right, level + 1)

```
