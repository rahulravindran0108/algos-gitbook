## Preorder traversal

Given a binary tree, return the preorder traversal of its nodes' values.

```
For example:
Given binary tree {1,#,2,3},
   1
    \
     2
    /
   3
return [1,2,3].
```
Note: Recursive solution is trivial, could you do it iteratively?

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        stack, result = [], []
        while stack or root:
            if root:
                stack.append(root)
                result.append(root.val)
                root = root.left
            else:
                root = stack.pop()
                root = root.right
        return result
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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        if(root == null) return result;

        Stack<TreeNode> stack = new Stack<TreeNode>();
        stack.add(root);

        while(!stack.isEmpty()) {
            TreeNode cur = stack.pop();
            result.add(cur.val);
            if(cur.right != null) stack.add(cur.right);
            if(cur.left != null) stack.add(cur.left);
        }

        return result;
    }
}
```
