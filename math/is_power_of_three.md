## Is Power of Three

Given an integer, write a function to determine if it is a power of three.

### Solution

```python
class Solution(object):
    def isPowerOfThree(self, n):
        """
        :type n: int
        :rtype: bool
        """
        if n == 0:
            return False
        if n == 1:
            return True

        while n % 3 == 0:
            if n == 3:
                return True
            n /= 3

        return False
```
