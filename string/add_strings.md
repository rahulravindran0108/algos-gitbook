## Add Strings

Given two non-negative numbers num1 and num2 represented as string, return the sum of num1 and num2.

Note:
```
The length of both num1 and num2 is < 5100.
Both num1 and num2 contains only digits 0-9.
Both num1 and num2 does not contain any leading zero.
You must not use any built-in BigInteger library or convert the inputs to integer directly.
```

### Solution

```python
class Solution(object):
    def addStrings(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        """
        len1, len2 = len(num1), len(num2)
        result = 0
        for i in xrange(len1):
            result += (ord(num1[i]) - 48) * 10 ** (len1 - i - 1)
        for i in xrange(len2):
            result += (ord(num2[i]) - 48) * 10 ** (len2 - i - 1)
        return str(result)        
```
