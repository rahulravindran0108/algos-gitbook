## Max Consecutive One

Given a binary array, find the maximum number of consecutive 1s in this array.

```
Example 1:
Input: [1,1,0,1,1,1]
Output: 3
```

Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.

### Solution

```java
public class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int globalMax = 0, localMax = 0;

        for(int i = 0;i<nums.length;i++) {
            if(nums[i] == 0) {
                globalMax = Math.max(globalMax, localMax);
                localMax = 0;
            } else
                localMax += 1;
        }

        globalMax = Math.max(globalMax, localMax);

        return globalMax;
    }
}
```
