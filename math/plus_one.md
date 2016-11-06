## Plus One

Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.

### Solution

```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        if not digits:
            return [1]
        t = digits.pop() + 1
        if t < 10:
            digits.append(t)
        else:
            t = t % 10
            digits = self.plusOne(digits)
            digits.append(t)
        return digits
```
