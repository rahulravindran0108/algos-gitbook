## Binary Tree Zigzag Level Order Traversal

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree `[3,9,20,null,null,15,7],`
```
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:
```
[
  [3],
  [20,9],
  [15,7]
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
    def zigzagLevelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if root is None:
            return []
        stack, result, flag = [root], [], False
        while stack:
            new_q = []
            nodes = [x.val for x in stack]
            if flag:
                nodes.reverse()
            result.append(nodes)
            for x in stack:
                if x.left:
                    new_q.append(x.left)
                if x.right:
                    new_q.append(x.right)
            stack, flag = new_q, not flag
        return result
```
