[题目介绍](https://leetcode.com/problems/linked-list-cycle-ii/)

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

To represent a cycle in the given linked list, we use an integer `pos` which represents the position (0-indexed) in the linked list where tail connects to. If `pos` is `-1`, then there is no cycle in the linked list.

**Note:** Do not modify the linked list.

**Example 1:**

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Example 2:**

```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Example 3:**

```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)







### 解法： hash

hashset来存放位置，如果有重复的说明就是环的起点。空间复杂度比较低。

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        unordered_set<ListNode *> nodeSet;
        while(head){
            if(nodeSet.find(head) != nodeSet.end()){
                return head;
            }
            nodeSet.insert(head);
            head = head -> next;
        }
        return NULL;
    }
};
```



### 解法：快慢指针

So this works because, if there exists a cycle in the linked list, the fast and slow pointer will surely meet atleast once, when the fast pointer has traversed an entire loop at least once.



So, let us say,



- the straight path before the cycle in the linked list is of length :
  **x**
- the place where slow and fast meet is **y** distance from the start of
  the cycle
- there are **z** steps left to reach the start of the cycle again from the
  meeting place



**slow pointer :**

travels `x + y` distance to meet the fast pointer



**fast pointer :**

travels `(x + y + (z + y))` distance to meet the slow pointer [reason : `(x + y)` to reach the meeting place, but it again goes around the loop and meets it on its way back, so `(z + y)` steps are needed]

But the fast pointer travels at speed 2 times that of slow pointer

So, `2(x + y) = (x + 2y + z)`
`=> x = z`

This is an extremely powerful result, which means that the distance between the start of the linked list and the start of the cycle, **x** is equal to the distance between the start of the cycle and the meeting point, **z**.

So, if slow walks at a step of 1 each time from the head of the list, and if fast walks at a pace of 1 step each time. They are to meet at the start of the cycle, because slow will travel **x** steps and fast will travel **z** steps.



```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            if (slow == fast) {
                slow = head;
                while(slow != fast){
                    slow = slow->next;
                    fast = fast->next;
                }
                return slow;
            }
        }
        return NULL;
        
    }
};
```

