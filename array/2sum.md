## Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.
```
Example:
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### Solution

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int [] result = {0, 0};
        HashMap<Integer, Integer> map = new HashMap<>();

        for(int i=0;i<nums.length; i ++) {
            map.put(target - nums[i], i);
        }

        for(int i=0;i<nums.length; i ++) {
            if(map.containsKey(nums[i])) {
                if( i == map.get(nums[i]))
                    continue;
                result[1] = map.get(nums[i]);
                result[0] = i;
                break;
            }
        }
        return result;
    }
}
```
