## 132 Pattern

Given a sequence of n integers a1, a2, ..., an, a 132 pattern is a subsequence ai, aj, ak such that i < j < k and ai < ak < aj. Design an algorithm that takes a list of n numbers as input and checks whether there is a 132 pattern in the list.

Note: n will be less than 15,000.

```
Example 1:
Input: [1, 2, 3, 4]

Output: False

Explanation: There is no 132 pattern in the sequence.
Example 2:
Input: [3, 1, 4, 2]

Output: True

Explanation: There is a 132 pattern in the sequence: [1, 4, 2].
Example 3:
Input: [-1, 3, 2, 0]

Output: True
```

Explanation: There are three 132 patterns in the sequence: [-1, 3, 2], [-1, 3, 0] and [-1, 2, 0].

### Solution

```python
class Solution(object):
    def find132pattern(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        stack = []
        for n in nums:
            if not stack or n < stack[-1][0]:
                stack.append((n, n))
            elif n > stack[-1][0]:
                last = list(stack.pop())
                if n < last[1]: return True
                else:
                    last[1] = n
                    while stack and n >= stack[-1][1]:
                        stack.pop()
                    if stack and n > stack[-1][0]: return True
                    stack.append(tuple(last))
        return False
```
