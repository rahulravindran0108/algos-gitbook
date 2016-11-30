## Candy

There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:
- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.

### Solution

```python
class Solution(object):
    def candy(self, ratings):
        """
        :type ratings: List[int]
        :rtype: int
        """
        if not ratings: return 0
        total, prev, cd = 1, 1, 0
        for i in range(1, len(ratings)):
            if ratings[i] >= ratings[i-1]:
                if cd > 0:
                    total += cd * (cd + 1) / 2
                    if cd >= prev:
                        total += cd - prev + 1
                    cd = 0
                    prev = 1
                prev = 1 if ratings[i] == ratings[i-1] else prev + 1
                total += prev
            else:
                cd += 1
        if cd > 0:
            total += cd * (cd + 1) / 2
            if cd >= prev:
                total += cd - prev + 1
        return total
```
