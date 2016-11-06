## Is Power of Two

Given an integer, write a function to determine if it is a power of two.

### Solution

```python
class Solution(object):
    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        if n == 0:
            return False
        if n == 1:
            return True

        while n % 2 == 0:
            if n == 2:
                return True
            n /= 2
        return False

```
