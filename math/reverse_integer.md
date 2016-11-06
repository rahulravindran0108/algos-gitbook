## Reverse Integer

Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

### Solution

```python
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        if x == 0 or x > sys.maxint or x < -sys.maxint:
            return 0

        result, sign =  "", 1
        if x < 0:
            x = -x
            sign = -1

        while x > 0:
            result += str(x % 10)
            x = x/10
        result = int(result)
        if result > 2147483647 or result < -2147483647:
            return 0
        return int(result) * sign

```
