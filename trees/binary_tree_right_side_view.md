## Binary Tree Right Side View

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

For example:
Given the following binary tree,
```
   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```
You should return `[1, 3, 4]`.


### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def rightSideView(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root is None:
            return []
        result, queue = [], [root]
        while queue:
            for r in range(len(queue)):
                top = queue.pop(0)
                if r == 0:
                    result.append(top.val)
                if top.right:
                    queue.append(top.right)
                if top.left:
                    queue.append(top.left)

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        dfs(root, result, 0);

        return result;
    }

    public void dfs(TreeNode root, List<Integer> result, int level) {
        if(root == null)
            return;
        if(level == result.size())
            result.add(root.val);
        dfs(root.right, result, level + 1);
        dfs(root.left, result, level + 1);
    }
}
```
