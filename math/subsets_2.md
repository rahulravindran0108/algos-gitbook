## Subsets 2

Given a collection of integers that might contain duplicates, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

```
For example,
If nums = [1,2,2], a solution is:

[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

### Solution

```java
public class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        dfs(nums, 0, new ArrayList<Integer>(), result);
        return result;
    }

    public void dfs(int [] nums, int index, List<Integer> path, List<List<Integer>> result) {
        result.add(path);

        for(int i = index;i < nums.length; i++) {
            if(i > index && nums[i] == nums[i-1]) continue;
            List<Integer> nPath = new ArrayList<Integer>(path);
            nPath.add(nums[i]);
            dfs(nums, i + 1, nPath, result);
        }
    }
}
```
