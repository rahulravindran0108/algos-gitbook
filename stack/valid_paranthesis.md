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


```java
public class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        for(int i = 0;i < s.length(); i++) {

            if(s.charAt(i) == '(' || s.charAt(i) == '{' || s.charAt(i) == '[')
                stack.push(s.charAt(i));
            else if(s.charAt(i) == ')' && !stack.empty() && stack.peek() == '(')
                stack.pop();
            else if(s.charAt(i) == '}' && !stack.empty() && stack.peek() == '{')
                stack.pop();
            else if(s.charAt(i) == ']' && !stack.empty() && stack.peek() == '[')
                stack.pop();
            else
                return false;
        }

        return stack.empty();
    }
}
```
