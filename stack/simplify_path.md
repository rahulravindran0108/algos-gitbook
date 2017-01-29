## Simplify Path

Given an absolute path for a file (Unix-style), simplify it.

For example,
```
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"
```

### Solution

```python
class Solution(object):
    def simplifyPath(self, path):
        """
        :type path: str
        :rtype: str
        """
        result = []
        parsed_path = path.split("/")
        for _ in parsed_path:
            if _ == "." or _ == "":
                continue
            elif _ == "..":
                if len(result) > 0:
                    result.pop()
            else:
                result.append(_)
        return "/" + "/".join(result)
```

```java
public class Solution {
    public String simplifyPath(String path) {
        Deque<String> dq = new LinkedList<>();
        Set<String> skip = new HashSet<>(Arrays.asList("..",".",""));

        for(String dir : path.split("/")) {
            if(dir.equals("..") && !dq.isEmpty()) dq.pop();
            else if(!skip.contains(dir)) dq.push(dir);
        }
        String res = "";

        for(String dir : dq)
            res = "/" + dir + res;

        return res.isEmpty() ? "/" : res;
    }
}
```
