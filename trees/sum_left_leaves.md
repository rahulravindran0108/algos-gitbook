## Sum of Left leaves

Find the sum of all left leaves in a given binary tree.

Example:
```
    3
   / \
  9  20
    /  \
   15   7
```

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sumOfLeftLeaves(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root is None:
            return 0
        if root.left and not root.left.right and not root.left.left:
            return root.left.val + self.sumOfLeftLeaves(root.right)
        return self.sumOfLeftLeaves(root.left) + self.sumOfLeftLeaves(root.right)
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
    public int sumOfLeftLeaves(TreeNode root) {
        int ans = 0;
        if(root == null) return ans;

        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);

        while(!stack.isEmpty()) {
            TreeNode cur = stack.pop();

            if(cur.left != null) {
                if(cur.left.left == null && cur.left.right == null)
                    ans += cur.left.val;
                else
                    stack.push(cur.left);
            }
            if(cur.right != null) {
                if(cur.right.left != null || cur.right.right != null)
                    stack.push(cur.right);
            }
        }

        return ans;
    }
}
```
