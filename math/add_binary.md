## Add Binary

Given two binary strings, return their sum (also a binary string).

```
For example,
a = "11"
b = "1"
Return "100".
```

### Solution

```python
class Solution(object):
    def addBinary(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: str
        """
        if len(a) < len(b):
            return self.addBinary(b, a)

        a = map(int, a)[::-1]
        b = map(int, b)[::-1]
        ans, carry = [], 0
        for i in range(len(a)):
            y = 0 if i >= len(b) else b[i]
            x = y + carry + a[i]
            ans.append(x % 2)
            carry = x / 2
        if carry:
            ans.append(carry)
        return "".join(map(str, ans[::-1]))


```
