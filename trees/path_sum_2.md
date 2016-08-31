## Path Sum 2

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:
Given the below binary tree and sum = 22,
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```
return
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: List[List[int]]
        """
        if root is None:
            return []
        result = []
        self.dfs(root, sum, result, [])
        return result

    def dfs(self, root, sum, result, tmp):
        if root is None:
            return
        if root.left is None and root.right is None and root.val == sum:
            tmp.append(root.val)
            result.append(list(tmp))
            tmp.pop()
        else:
            tmp.append(root.val)
            if root.left:
                self.dfs(root.left, sum - root.val, result, tmp)
            if root.right:
                self.dfs(root.right, sum - root.val, result, tmp)
            tmp.pop()
```
