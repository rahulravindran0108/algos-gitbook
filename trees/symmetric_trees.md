## Symmetric Trees

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following [1,2,2,null,3,null,3] is not:
```
    1
   / \
  2   2
   \   \
   3    3
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
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root:
            return self.helper(root, root)
        return True

    def helper(self, left, right):
        if left is None and right is None:
            return True
        if left and right and left.val == right.val:
            return self.helper(left.left, right.right) and self.helper(left.right, right.left)
        return False
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
    public boolean isSymmetric(TreeNode root) {
        if(root == null) return true;
        return helper(root, root);
    }

    public boolean helper(TreeNode left, TreeNode right) {
        if(left == null && right == null) return true;
        if(left != null && right != null && left.val == right.val)
            return helper(left.left, right.right) && helper(left.right, right.left);
        return false;
    }
}
```
