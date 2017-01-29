## Compare Version Number

### Solution

```python
class Solution(object):
    def compareVersion(self, version1, version2):
        """
        :type version1: str
        :type version2: str
        :rtype: int
        """
        v1 = list(map(int, version1.split(".")))
        v2 = list(map(int, version2.split(".")))
        size = max(len(v1), len(v2))

        for i in range(size):
            n1 = v1[i] if i < len(v1) else 0
            n2 = v2[i] if i < len(v2) else 0

            if n1 > n2:
                return 1
            if n1 < n2:
                return -1
        return 0

```

```java
public class Solution {
    public int compareVersion(String version1, String version2) {
        String[] levels1 = version1.split("\\.");
        String[] levels2 = version2.split("\\.");

        int length = Math.max(levels1.length, levels2.length);
        for (int i=0; i<length; i++) {
        	Integer v1 = i < levels1.length ? Integer.parseInt(levels1[i]) : 0;
        	Integer v2 = i < levels2.length ? Integer.parseInt(levels2[i]) : 0;
        	int compare = v1.compareTo(v2);
        	if (compare != 0) {
        		return compare;
        	}
        }

        return 0;

    }
}
```
