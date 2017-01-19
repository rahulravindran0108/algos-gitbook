## Recover Binary Search Tree

Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

Note:
A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

## Solution

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def recoverTree(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        self.n1 = self.n2 = self.prev = None
        self.findNodes(root)
        self.n1.val, self.n2.val = self.n2.val, self.n1.val

    def findNodes(self, root):
        if root:
            self.findNodes(root.left)
            if self.prev and self.prev.val > root.val:
                self.n2 = root
                if self.n1 == None: self.n1 = self.prev
            self.prev = root
            self.findNodes(root.right)
```


```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void recoverTree(TreeNode root) {
        TreeNode pre = null, first = null, second = null, temp = null;

        while(root != null) {
            if(root.left != null) {
                temp = root.left;

                while(temp.right != null && temp.right != root)
                    temp = temp.right;

                if(temp.right == null) {
                    temp.right = root;
                    root = root.left;
                } else {
                    if(pre!=null && pre.val > root.val){
				        if(first==null){first = pre;second = root;}
				        else{second = root;}
				    }
				    pre = root;
				    temp.right = null;
					root = root.right;
                }

            } else {
                if(pre != null && pre.val > root.val) {
                    if(first == null) {
                        first = pre;
                        second = root;
                    } else second = root;
                }
                pre = root;
                root = root.right;
            }
        }

        // swap two node values;
		if(first!= null && second != null){
		    int t = first.val;
		    first.val = second.val;
		    second.val = t;
		}
    }
}
```
