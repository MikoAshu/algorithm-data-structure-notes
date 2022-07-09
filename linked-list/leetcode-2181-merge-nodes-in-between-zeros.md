# LeetCode 2181 - Merge Nodes in Between Zeros

<mark style="background-color:orange;">Medium</mark>

You are given the `head` of a linked list, which contains a series of integers **separated** by `0`'s. The **beginning** and **end** of the linked list will have `Node.val == 0`.

For **every** two consecutive `0`'s, **merge** all the nodes lying in between them into a single node whose value is the **sum** of all the merged nodes. The modified list should not contain any `0`'s.

Return _the_ `head` _of the modified linked list_.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2022/02/02/ex1-1.png)

```
Input: head = [0,3,1,0,4,5,2,0]
Output: [4,11]
Explanation: 
The above figure represents the given linked list. The modified list contains
- The sum of the nodes marked in green: 3 + 1 = 4.
- The sum of the nodes marked in red: 4 + 5 + 2 = 11.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2022/02/02/ex2-1.png)

```
Input: head = [0,1,0,3,0,2,2,0]
Output: [1,3,4]
Explanation: 
The above figure represents the given linked list. The modified list contains
- The sum of the nodes marked in green: 1 = 1.
- The sum of the nodes marked in red: 3 = 3.
- The sum of the nodes marked in yellow: 2 + 2 = 4.
```

&#x20;

**Constraints:**

* The number of nodes in the list is in the range `[3, 2 * 105]`.
* `0 <= Node.val <= 1000`
* There are **no** two consecutive nodes with `Node.val == 0`.
* The **beginning** and **end** of the linked list have `Node.val == 0`.

## Solution

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeNodes(ListNode head) {
        ListNode dummy = new ListNode();
        dummy.next = head;
        ListNode l = dummy.next, r = dummy.next.next;
        
        while(r != null) {
            // place the left at 0 node and add the values till the next 0 node
            l.val += r.val;
            // when you find a 0 node on the right, move the left to that node
            if(r.val == 0) {
                // if the right node at 0 has no next, just point the left node to null as we have completed our computation
                if(r.next == null) {
                    l.next = null;
                } else {
                    l.next = r;
                }
                
                l = r;
                r = r.next;
            } else {
                // else move the right node
                r = r.next;
            }
        }
        // set the nodes to null for good measure 
        l.next = null;
         l=null;
        r = null;
        // no need for dummy as we are not touching the head at any point
        return head;
    }
}
```
