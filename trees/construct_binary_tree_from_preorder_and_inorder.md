## Construct Binary Tree from Preorder and Inorder

Given preorder and inorder traversal of a tree, construct the binary tree.

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        if len(preorder) == 0:
            return None
        stack, root, index = [], TreeNode(preorder[0]), 0
        stack.append(root)
        for i in range(1, len(preorder)+1):
            cur = stack[-1]
            if cur.val != inorder[index]:
                cur.left = TreeNode(preorder[i])
                stack.append(cur.left)
            else:
                while len(stack) != 0 and stack[-1].val == inorder[index]:
                    cur = stack[-1]
                    stack.pop()
                    index +=1

                if index<len(inorder):
                    cur.right=TreeNode(preorder[i])
                    stack.append(cur.right)
            i+=1
        return root
```
