## Length of Last Word

Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example,
Given s = "Hello World",
return 5.

### Solution

```python
class Solution(object):
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s:
            return 0
        return len(s.strip().split(' ')[-1])

```

```java
public class Solution {
    public int lengthOfLastWord(String s) {

        if(s == null || s.length() == 0)
            return 0;

        String [] words = s.split("\\s+");

        return words.length == 0 ? 0 : words[words.length -1].length();
    }
}
```
