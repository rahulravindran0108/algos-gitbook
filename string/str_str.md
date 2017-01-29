## strStr()

Implement strStr().

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

### Solution

```python
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        return haystack.find(needle)
```

```java
public class Solution {

    //KMP
    public int strStr(String haystack, String needle) {

        if(needle.equals("")) return 0;
	    if(haystack.equals("")) return -1;

        char [] arr = needle.toCharArray();
        int [] prefix = makeNext(arr);

        for(int i = 0, j = 0, end = haystack.length(); i < end;) {

    		if(haystack.charAt(i) == arr[j]) {
    			j++;
    			i++;
    			if(j == arr.length) return i - arr.length;
    		}

    		if(i < end && haystack.charAt(i) != arr[j]) {
    		    if(j == 0)
    		        i++;
    		    else
    		        j = j == 0 ? 0 : prefix[j-1];
    		}

    	}

    	return -1;
    }

    private int [] makeNext(char [] arr) {
        int len = arr.length;

        int [] prefix = new int[len];
        prefix[0] = 0;
        int j = 0;

        for(int i  = 1;i<len;i++) {
            if(arr[i] == arr[j]) {
                prefix[i] = j + 1;
                j++;
            } else {

                if(j == 0)
                    prefix[i] = 0;
                else {
                    while(j> 0 && arr[i] != arr[j])
                        j = prefix[j-1];

                    if(arr[i] != arr[j])
                        prefix[i] = 0;
                    else {
                        prefix[i] = prefix[j] + 1;
                        j++;
                    }
                }
            }
        }

        return prefix;
    }
}
```
