## Add Binary

Given two binary strings, return their sum (also a binary string).

```
For example,
a = "11"
b = "1"
Return "100".
```

### Solution

```python
class Solution(object):
    def addBinary(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: str
        """
        if len(a) < len(b):
            return self.addBinary(b, a)

        a = map(int, a)[::-1]
        b = map(int, b)[::-1]
        ans, carry = [], 0
        for i in range(len(a)):
            y = 0 if i >= len(b) else b[i]
            x = y + carry + a[i]
            ans.append(x % 2)
            carry = x / 2
        if carry:
            ans.append(carry)
        return "".join(map(str, ans[::-1]))

```

```java
public class Solution {
    public String addBinary(String a, String b) {
        StringBuilder sb = new StringBuilder();

        int i = a.length() - 1, j = b.length() - 1;
        int carry = 0;

        while(i >= 0 || j >= 0) {
            int sum = carry;
            if(i >= 0) sum += a.charAt(i--) - '0';
            if(j >= 0) sum += b.charAt(j--) - '0';

            sb.append(sum % 2);
            carry = sum / 2;
        }

        if(carry != 0) sb.append(carry);
        return sb.reverse().toString();
    }
}
```
