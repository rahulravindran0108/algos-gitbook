## Ransom Note

Given  an  arbitrary  ransom  note  string  and  another  string  containing  letters from  all  the  magazines,  write    function  that  will  return  true  if  the  ransom  note  can  be  constructed  from  the  magazines;  otherwise,  it  will  return  false.  

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
