## Combination Sum 2

Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

Note:
All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
For example, given candidate set [10, 1, 2, 7, 6, 1, 5] and target 8,
A solution set is:
```
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

### Solution

```python
class Solution(object):
    def combinationSum2(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        result = []
        self.csum_recurse(sorted(candidates), result, [], 0, target)
        return result

    def csum_recurse(self, candidates, result, intermediate, start, target):
        if target == 0:
            result.append(list(intermediate))
        prev = 0
        while start < len(candidates) and candidates[start] <= target:
            if prev != candidates[start]:
                intermediate.append(candidates[start])
                self.csum_recurse(candidates, result, intermediate, start + 1, target - candidates[start])
                intermediate.pop()
                prev = candidates[start]
            start += 1
```

```java
public class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates);
        dfs(candidates, target, result, new ArrayList<>(), 0);
        return result;
    }


    public void dfs(int [] candidates, int target, List<List<Integer>> result, List<Integer> path, int start) {
        if(target < 0 ) return;
        if(target == 0 ) result.add(new ArrayList<>(path));
        else {
            for(int i = start;i<candidates.length;i++) {
                if(i > start && candidates[i] == candidates[i-1]) continue;
                path.add(candidates[i]);
                dfs(candidates, target - candidates[i], result, path, i + 1);
                path.remove(path.size() - 1);
            }
        }
    }
}
```
