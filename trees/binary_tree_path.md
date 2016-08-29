## Binary Tree Path

Given a binary tree, return all root-to-leaf paths.

For example, given the following binary tree:
```
   1
 /   \
2     3
 \
  5
```
All root-to-leaf paths are:
```
["1->2->5", "1->3"]
```

### Solution

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    # @param {TreeNode} root
    # @return {string[]}
    def binaryTreePaths(self, root):
        if root is None:
            return []
        result, tmp = [], []
        self.dfs(root, result, tmp)
        return result

    def dfs(self, root, result, tmp):
        if root.right is None and root.left is None:
            tmp.append(root.val)
            result.append("->".join(str(x) for x in tmp))
            tmp.pop()
        else:
            tmp.append(root.val)
            if root.left:
                self.dfs(root.left, result, tmp)
            if root.right:
                self.dfs(root.right, result, tmp)
            tmp.pop()
```
