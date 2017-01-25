## Reverse String

Write a function that takes a string as input and returns the string reversed.

Example:
Given s = "hello", return "olleh".

### Solution

```java
public class Solution {
    public String reverseString(String s) {
        char [] arr = s.toCharArray();

        int i = 0, j = arr.length - 1;

        while(i < j) {
            char temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
            j--;
        }

        return new String(arr);
    }
}
```
