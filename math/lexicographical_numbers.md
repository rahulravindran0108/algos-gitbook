## Lexicographical Numbers

Given an integer n, return 1 - n in lexicographical order.

For example, given 13, return: [1,10,11,12,13,2,3,4,5,6,7,8,9].

Please optimize your algorithm to use less time and space. The input size may be as large as 5,000,000.

### Solution

```python
class Solution(object):
    def lexicalOrder(self, n):
        """
        :type n: int
        :rtype: List[int]
        """
        stack, result, x = [], [], 1
        while x<= n:
            stack.append(x)
            result.append(x)
            x *= 10
        while stack:
            y = stack.pop()
            if y%10 == 9: continue
            y+=1
            while y<= n:
                stack.append(y)
                result.append(y)
                y *=10
        return result
```
