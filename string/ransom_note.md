## Ransom Note

Ransom note problem on Leetcode.
### Solution

```python
class Solution(object):
    def canConstruct(self, ransomNote, magazine):
        """
        :type ransomNote: str
        :type magazine: str
        :rtype: bool
        """
        for ch in ransomNote:
            index = -1
            try:
                index = magazine.index(ch)
            except ValueError:
                index = -1
            if index == -1:
                return False
            magazine = magazine[:index] + magazine[index+1:]
        return True

```
