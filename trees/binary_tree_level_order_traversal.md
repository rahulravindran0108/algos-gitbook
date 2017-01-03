## Binary Tree Level Order Traversal

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,
```
    3
   / \
  9  20
    /  \
   15   7
```
return its level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
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
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if root is None:
            return []
        stack, result = [root], []
        while stack:
            new_q = []
            result.append([x.val for x in stack])
            for node in stack:
                if node.left:
                    new_q.append(node.left)
                if node.right:
                    new_q.append(node.right)
            stack = new_q
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if(root == null) return result;
        List<TreeNode> stack = new ArrayList<>();
        stack.add(root);

        while(!stack.isEmpty()) {
            List<TreeNode> loc = new ArrayList<>(); // local list
            result.add(stack.stream()
                            .map(item -> item.val)
                            .collect(Collectors.toList()));

            stack.forEach(node -> {
               if(node.left != null) loc.add(node.left);
               if(node.right != null) loc.add(node.right);
            });

            stack = loc;
        }

        return result;
    }
}
```
