## Valid Paranthesis

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

Subscribe to see which companies asked this question

### Solution

```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if len(s) % 2 != 0:
            return False
        stack = []
        for i,v in enumerate(s):
            if v == "(" or v == "{" or v == "[":
                stack.append(v)
            elif len(stack) == 0:
                pass
            elif (v == ")" and stack[-1] == "(") or (v =="]" and stack[-1] == "[") or (v == "}" and stack[-1] == "{"):
                stack.pop()
        return not stack
```
