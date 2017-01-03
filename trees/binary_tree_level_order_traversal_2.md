## Binary Tree Level Order Traversal 2

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree `[3,9,20,null,null,15,7],`
```
    3
   / \
  9  20
    /  \
   15   7
```
return its bottom-up level order traversal as:
```
[
  [15,7],
  [9,20],
  [3]
]
```

## Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrderBottom(self, root):
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
        return result[::-1]
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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        List<List<Integer>> result = new ArrayList<>();

        if(root == null) return result;
        queue.add(root);

        while(!queue.isEmpty()) {
            int sz = queue.size();
            List<Integer> subList = new ArrayList<>();

            for(int i = 0;i<sz;i++) {
                if(queue.peek().left != null) queue.offer(queue.peek().left);
                if(queue.peek().right != null) queue.offer(queue.peek().right);
                subList.add(queue.poll().val);
            }

            result.add(0, subList);
        }

        return result;

    }
}
```
