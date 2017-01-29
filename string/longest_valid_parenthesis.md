## Longest Valid Parentheses

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

For "(()", the longest valid parentheses substring is "()", which has length = 2.

Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.

Subscribe to see which companies asked this question

### Solution

```python
class Solution(object):
    def longestValidParentheses(self, s):
        """
        :type s: str
        :rtype: int
        """
        stack, max_length, left = [], 0, {}
        for i, c in enumerate(s):
            if c == "(":
                stack.append(i)
            elif stack:
                l = stack.pop()
                r = i
                if left.has_key(l-1):
                    left[r] = left[l-1]
                else:
                    left[r] = l
                if r - left[r] + 1 > max_length:
                    max_length = r - left[r] + 1
        return max_length
```

```java
public class Solution {
    public int longestValidParentheses(String s) {
        Stack<Integer> stack = new Stack<>();
        int left = -1, max = 0;

        for(int i = 0;i<s.length();i++) {
            if(s.charAt(i) == '(')
                stack.push(i);
            else {
                if(stack.isEmpty()) left = i;
                else {
                    stack.pop();
                    if(stack.isEmpty()) max = Math.max(max, i - left);
                    else max = Math.max(max, i - stack.peek());
                }
            }
        }

        return max;
    }
}
```
