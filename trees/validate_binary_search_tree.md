## Validate Binary Search Tree

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
Example 1:
```
    2
   / \
  1   3
```
Binary tree [2,1,3], return true.
Example 2:
```
    1
   / \
  2   3
```
Binary tree [1,2,3], return false.

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        infinity = 10 ** 10
        return self.validateTree(root, -infinity, infinity)

    def validateTree(self, root, min, max):
        if root is None:
            return True
        if root.val <= min or root.val >= max:
            return False
        return self.validateTree(root.left, min, root.val) and self.validateTree(root.right, root.val, max)
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public boolean isValidBST(TreeNode root) {
        if(root == null) return true;
        return helper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean helper(TreeNode root, long lb, long ub) {
        if(root == null) return true;

        if(root.val <= lb || root.val >= ub)
            return false;

        return helper(root.left, lb, root.val) && helper(root.right, root.val, ub);
    }
}
```
