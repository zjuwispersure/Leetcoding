[题目介绍](https://leetcode.com/problems/intersection-of-two-linked-lists/)

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

[![img](https://assets.leetcode.com/uploads/2018/12/13/160_statement.png)](https://assets.leetcode.com/uploads/2018/12/13/160_statement.png)

begin to intersect at node c1.

 

**Example 1:**

[![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
Output: Reference of the node with value = 8
Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

 

**Example 2:**

[![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

```
Input: intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
Output: Reference of the node with value = 2
Input Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [0,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
```

 

**Example 3:**

[![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

```
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: null
Input Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
```

 

**Notes:**

- If the two linked lists have no intersection at all, return `null`.
- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in O(n) time and use only O(1) memory.



###  解法

如果有交集，那么尾部的元素一定一样的，因此可以让两个list变成等长的(长的多往后走几步)，然后依次比较即可。

下面这个代码是第一波自己写的，感觉有些冗余。

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        int lengthA = 0;
        int lengthB = 0;
        ListNode* newHeadA = headA;
        ListNode* newHeadB = headB;
        while(newHeadA){
            lengthA++;
            newHeadA = newHeadA->next;
        }
        while(newHeadB){
            lengthB++;
            newHeadB = newHeadB->next;
        }
        if(lengthA > lengthB){
            for(int i = 0 ; i < lengthA - lengthB; i++){
                headA = headA->next;
            }
        }
        if(lengthB > lengthA){
            for(int i = 0 ; i < lengthB - lengthA; i++){
                headB = headB->next;
            }
        }
        while(headA != headB && headA && headB){
            headA = headA->next;
            headB = headB->next;
        }
        return headA;
        
    }
};
```

