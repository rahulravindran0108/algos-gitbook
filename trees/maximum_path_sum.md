## Binary Tree Maximum Path Sum

Given a binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path does not need to go through the root.

For example:
Given the below binary tree,
```
       1
      / \
     2   3
```
Return `6`.

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxPathSum(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        maxSum, _ = self.maxPathSumHelper(root)
        return maxSum

    def maxPathSumHelper(self, root):
        if root is None:
            return -sys.maxint, 0
        left = self.maxPathSumHelper(root.left)
        right = self.maxPathSumHelper(root.right)
        maxpath = max(left[0], right[0], root.val + left[1] + right[1])
        single = max(left[1] + root.val, right[1] + root.val, 0)
        return maxpath, single
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

    int maxValue;

    public int maxPathSum(TreeNode root) {
        maxValue = Integer.MIN_VALUE;
        dfs(root);
        return maxValue;
    }

    public int dfs(TreeNode root) {
        if(root == null) return 0;
        int left = Math.max(0, dfs(root.left));
        int right = Math.max(0, dfs(root.right));
        maxValue = Math.max(maxValue, left + right + root.val);

        return Math.max(left, right) + root.val;
    }
}
```
