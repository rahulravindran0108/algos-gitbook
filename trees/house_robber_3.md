## House Robber 3

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

Example 1:
```
     3
    / \
   2   3
    \   \
     3   1
```
Maximum amount of money the thief can rob = `3 + 3 + 1 = 7`.
Example 2:
```
     3
    / \
   4   5
  / \   \
 1   3   1
```
Maximum amount of money the thief can rob = `4 + 5 = 9`.


### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def rob(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        return max(self.robHelper(root))

    def robHelper(self, root):
        if not root:
            return (0, 0)
        left, right = self.robHelper(root.left), self.robHelper(root.right)
        return (root.val + left[1] + right[1], max(left) + max(right))
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
    public int rob(TreeNode root) {
        int [] res = dfs(root);
        return Math.max(res[0], res[1]);
    }

    public int [] dfs(TreeNode root) {
        if(root == null) return new int[2];

        int [] left = dfs(root.left);
        int [] right = dfs(root.right);

        int [] res = new int[2];

        res[0] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
        res[1] = root.val + left[0] + right[0];

        return res;
    }
}
```
