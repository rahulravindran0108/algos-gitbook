## Shortest Palindrome

Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

```
For example:

Given "aacecaaa", return "aaacecaaa".

Given "abcd", return "dcbabcd".
```

### Solution

```python
class Solution(object):
    def shortestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        table = s + "*" + s[::-1]
        cont = [0]
        for i in range(1,len(table)):
            index = cont[i-1]
            while index > 0 and table[index] != table[i]:
                index = cont[index -1]
            cont.append(index + (1 if table[index] == table[i] else 0))
        return s[cont[-1]:][::-1]+s
```

```java
public class Solution {
    public String shortestPalindrome(String s) {
        String temp = s + "#" + new StringBuilder(s).reverse().toString();
        int [] table = getTable(temp);
        return new StringBuilder(s.substring(table[table.length - 1])).reverse().toString() + s;
    }

    private int [] getTable(String s) {
        int [] table = new int[s.length()];

        int index = 0;

        for(int i = 1;i<s.length();i++) {

            if(s.charAt(index) == s.charAt(i)) {
                table[i] = table[i-1] + 1;
                index++;
            } else {
                index = table[i-1];

                while(index > 0 && s.charAt(index) != s.charAt(i))
                    index = table[index-1];

                if(s.charAt(i) == s.charAt(index))
                    index++;

                table[i] = index;
            }
        }

        return table;
    }
}
```
