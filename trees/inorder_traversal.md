## Inorder Traversal

Given a binary tree, return the inorder traversal of its nodes' values.

For example:
```
Given binary tree [1,null,2,3],
   1
    \
     2
    /
   3
return [1,3,2].
```

### Solution

Recursive Approach:

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        result = []
        self.inorder(root, result)
        return result

    def inorder(self, root, result):
        if root is None:
            return None
        self.inorder(root.left, result)
        result.append(root.val)
        self.inorder(root.right, result)
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;

        while(cur != null || !stack.isEmpty()) {
            while(cur != null) {
                stack.add(cur);
                cur = cur.left;
            }

            cur = stack.pop();
            result.add(cur.val);
            cur = cur.right;
        }

        return result;
    }
}
```
