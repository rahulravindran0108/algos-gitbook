## Jesse Loves Candy

Jessie loves candy so much that she buys it from  different stores every day. Her city is located along a number line. It has  buildings, , and each  is located at coordinate . Each building has a candy value of either 1 or 0, where  denotes a candy shop and  denotes a regular building that does not sell candy. Jessie lives in building , so the candy value of this location is always .

Jessie always starts out from her house, , and buys her candies from  different shops. It takes her  second to move a distance of  unit when her hands are empty; once she makes her first candy purchase, it takes her seconds to move a distance of  unit.

Given the candy value of each building in the city, find and print the minimum amount of time needed for Jessie to visit two candy shops if she starts from her house at coordinate .

https://www.hackerrank.com/contests/adobe-codhers/challenges/jesse-loves-candy

### Solution

```python
# Enter your code here. Read input from STDIN. Print output to STDOUT
import sys

n, k = map(int, raw_input().strip().split())
arr = map(int, raw_input().strip().split())
index, max_value = list(), sys.maxint

index =[i for i in range(len(arr)) if arr[i] == 1]


for i in range(1, len(index)):
    if index[i - 1] + (index[i] - index[i - 1]) * k < max_value:
        max_value = index[i - 1] + (index[i] - index[i - 1]) * k

print max_value
```
