## Most Frequent Subtree Sum

Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.

```
Examples 1
Input:

  5
 /  \
2   -3
return [2, -3, 4], since all the values happen only once, return all of them in any order.
Examples 2
Input:

  5
 /  \
2   -5
return [2], since 2 happens twice, however -5 only occur once.
```

### Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

from collections import Counter

class Solution(object):
    def findFrequentTreeSum(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root is None:
            return list()

        res = Counter()
        self.dfs(res, root)
        most_freq = res.most_common(1)[0][1]

        return [x[0] for x in res.most_common() if x[1] == most_freq]

    def dfs(self, path, root):
        if root is None:
            return 0

        l = self.dfs(path, root.left)
        r = self.dfs(path, root.right)

        path.update([l + r + root.val])

        return l + r + root.val
```
