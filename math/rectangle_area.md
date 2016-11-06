## Rectangle Area

Find the total area covered by two rectilinear rectangles in a 2D plane.

Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.


### Solution

```python
class Solution(object):
    def computeArea(self, A, B, C, D, E, F, G, H):
        """
        :type A: int
        :type B: int
        :type C: int
        :type D: int
        :type E: int
        :type F: int
        :type G: int
        :type H: int
        :rtype: int
        """
        area_1 = (C-A) * (D-B)
        area_2 = (G-E) * (H-F)

        diff_x = min(G, C) - max(E, A)
        diff_y = min(D, H) - max(B, F)

        return area_1 + area_2 - (diff_x * diff_y if diff_y >= 0 and diff_x >= 0 else 0)
```
