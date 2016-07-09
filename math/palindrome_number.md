## Palindrome Number

Determine whether an integer is a palindrome. Do this without extra space.

## Solution

```python
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        div = 1
        while x/div >= 10:
            div = div * 10
        
        while x:
            left = x / div
            right = x % 10
            if left != right:
                return False
            x = (x % div) / 10
            div = div / 100
        return True
```