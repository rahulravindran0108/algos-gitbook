## Valid Anagram

Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
```
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.
```

### Solution

```python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        for letter in set(s+t):
            if s.count(letter) != t.count(letter):
                return False
        return True
```

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        char [] sArr = s.toCharArray();
        char [] tArr = t.toCharArray();

        Arrays.sort(sArr);
        Arrays.sort(tArr);

        return String.valueOf(sArr).equals(String.valueOf(tArr));
    }
}
```
