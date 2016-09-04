## Construct Binary Tree from Inorder and Postorder Traversal

Given inorder and postorder traversal of a tree, construct the binary tree.

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def buildTree(self, inorder, postorder):
        """
        :type inorder: List[int]
        :type postorder: List[int]
        :rtype: TreeNode
        """
        if len(postorder) == 0:
            return None
        stack, index = [], len(postorder) - 1
        root = TreeNode(postorder[index])
        stack.append(root)
        for i in range(len(postorder) - 2, -1, -1):
            cur = stack[-1]
            if cur.val != inorder[index]:
                cur.right = TreeNode(postorder[i])
                stack.append(cur.right)
            else:
                while len(stack) != 0 and stack[-1].val == inorder[index]:
                    cur = stack[-1]
                    stack.pop()
                    index -= 1
                if index >= 0:
                    cur.left = TreeNode(postorder[i])
                    stack.append(cur.left)
            i -= 1
        return root
```
