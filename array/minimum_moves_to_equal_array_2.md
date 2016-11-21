## Minimum Number of Moves to Equal Array 2

Given a non-empty integer array, find the minimum number of moves required to make all array elements equal, where a move is incrementing a selected element by 1 or decrementing a selected element by 1.

You may assume the array's length is at most 10,000.
```
Example:

Input:
[1,2,3]

Output:
2

Explanation:
Only two moves are needed (remember each move increments or decrements one element):

[1,2,3]  =>  [2,2,3]  =>  [2,2,2]
```

### Solution

```python
class Solution(object):
    def minMoves2(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        mid = self.q_select(nums, len(nums) >> 1)
        ans = 0
        for i in nums:
            ans += abs(mid - i)
        return ans

    def q_select(self, n, tar):
        def select(n, l, r, tar):
            if l == r: return n[l]

            p = random.randint(l, r)

            n[l], n[p] = n[p], n[l]

            i = l
            for j in range(l+1, r+1):
                if n[j] < n[l]:
                    i += 1
                    n[i], n[j] = n[j], n[i]

            n[i], n[l] = n[l], n[i]

            if i == tar: return n[i]
            elif i > tar: return select(n, l, i - 1, tar)
            else: return select(n, i+1, r, tar)

        return select(n, 0, len(n) - 1, tar)
```
