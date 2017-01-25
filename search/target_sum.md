## Target Sum

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

```
Example 1:
Input: nums is [1, 1, 1, 1, 1], S is 3.
Output: 5
Explanation:

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```

There are 5 ways to assign symbols to make the sum of nums be target 3.

### Solution

```java
public class Solution {
    int result = 0;

    public int findTargetSumWays(int[] nums, int S) {
        if(nums == null || nums.length == 0)
            return result;

        int n = nums.length;
        int [] sum = new int[n];
        sum[n-1] = nums[n-1];

        for(int i = n-2;i>=0;i--) {
            sum[i] += sum[i+1] + nums[i];
        }

        dfs(nums,sum,0,S);

        return result;

    }

    public void dfs(int [] nums, int [] sums, int pos, int target) {
        if(pos == nums.length) {
            if(target == 0)
                result++;
            return;
        }

        if(sums[pos] < Math.abs(target))
            return;

        dfs(nums, sums, pos + 1, target - nums[pos]);
        dfs(nums, sums, pos + 1, target + nums[pos]);
    }
}
```
