## Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
```
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.
```

Note:
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

### Solution

```python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        s = ''.join([i.lower() for i in s if i.isalnum()])
        return s == s[::-1]

```

```java
public class Solution {
    public boolean isPalindrome(String s) {
        int i = 0, j = s.length() - 1;

        while(i < j) {
            while(i < j && !Character.isLetterOrDigit(s.charAt(i))) i ++;
            while(i < j && !Character.isLetterOrDigit(s.charAt(j))) j --;
            if(Character.toLowerCase(s.charAt(i)) == Character.toLowerCase(s.charAt(j))) {
                i++;j--;
            } else return false;
        }
        return true;
    }
}
```
