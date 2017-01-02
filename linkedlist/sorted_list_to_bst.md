## Convert Sorted List to BST

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

### Solution

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        array = []
        p = head
        while p:
            array.append(p.val)
            p = p.next
        return self.sortedArrayToBST(array)

    def sortedArrayToBST(self, array):
        length = len(array)
        if length == 0:
            return None
        elif length == 1:
            return TreeNode(array[0])
        root = TreeNode(array[length/2])
        root.left = self.sortedArrayToBST(array[:length/2])
        root.right = self.sortedArrayToBST(array[length/2+1:])
        return root
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
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
    public TreeNode sortedListToBST(ListNode head) {
        if(head == null)
            return null;
        return toBST(head, null);
    }

    public TreeNode toBST(ListNode head, ListNode tail) {
        ListNode fast = head, slow = head;

        if(head == tail) return null;

        while(fast != tail && fast.next != tail) {
            fast = fast.next.next;
            slow = slow.next;
        }

        TreeNode thead = new TreeNode(slow.val);

        thead.right = toBST(slow.next, tail);
        thead.left= toBST(head, slow);

        return thead;
    }
}
```
