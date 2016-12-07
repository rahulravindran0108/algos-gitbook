## Subset

Given a set of distinct integers, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

```
For example,
If nums = [1,2,3], a solution is:

[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

### Solution

```java
public class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        dfs(nums, 0, new ArrayList<Integer>(), result);
        return result;
    }

    public void dfs(int [] nums, int index, List<Integer> path, List<List<Integer>> result) {
        result.add(path);
        for(int i = index; i < nums.length;i ++) {
            List<Integer> nPath = new ArrayList<Integer>(path);
            nPath.add(nums[i]);
            dfs(nums, i + 1, nPath, result);
        }
    }
}
```
