## Generate Paranthesis

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

### Solution

```python
class Solution(object):
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        res = list()
        self.dfs("", n, n, res)
        return res

    def dfs(self, prefix, left, right, res):
        if left == 0 and right == 0:
            res.append(prefix)

        if left > 0: self.dfs(prefix + "(", left - 1, right, res)
        if left < right: self.dfs(prefix + ")", left, right - 1, res)
```
