## Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

### Solution

```python
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs:
            return ""
        base_str = strs[0]

        for i in range(len(base_str)):
            for j in strs:
                if i >= len(j) or base_str[i] != j[i]:
                    return base_str[:i]
        return base_str
```

```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {

        if(strs == null || strs.length == 0)
            return "";

        StringBuilder sb = new StringBuilder();
        String base = strs[0];

        for(int i = 0;i < base.length();i++) {
            char c = base.charAt(i);

            for(String s : strs) {
                if(s.length() < i + 1 || c != s.charAt(i)) return sb.toString();
            }
            sb.append(c);
        }

        return sb.toString();
    }
}
```
