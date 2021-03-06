## Balanced Binary Tree

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root is None:
            return True
        if abs(self.helper(root.left) - self.helper(root.right)) <= 1:
            return self.isBalanced(root.left) and self.isBalanced(root.right)
        else:
            return False

    def helper(self, root):
        if root is None:
            return 0
        return max(self.helper(root.left), self.helper(root.right)) + 1
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
    public boolean isBalanced(TreeNode root) {
        if(root == null)
            return true;
        return dfs(root) == -1 ? false : true;
    }

    public int dfs(TreeNode root) {
        if(root == null)
            return 0;

        int left = dfs(root.left);
        int right = dfs(root.right);

        if(left == -1 || right == -1)
            return -1;
        return Math.abs(left - right) > 1 ? -1 : 1 + Math.max(left, right);
    }
}
```
