## String to Integer

Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.


### Solution

```python
class Solution(object):
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        r = re.match("[+-]?[0-9]+", str.strip())
        if not r:
            return 0
        y = int(r.group())
        if y < -2147483648:
            y = -2147483648
        if y > 2147483647:
            y = 2147483647
        return y
```
