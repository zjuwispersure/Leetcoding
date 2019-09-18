[题目介绍](https://leetcode.com/problems/majority-element/)

Given an array of size *n*, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```
Input: [3,2,3]
Output: 3
```

**Example 2:**

```
Input: [2,2,1,1,1,2,2]
Output: 2
```



### 解法：栈

之前《编程之美》看过类似的问题，解法有很多，记得比较巧妙的一种是用栈来记录内容，每个元素来的时候如果和栈顶元素不一样就弹出，相同则入栈。最后栈中剩余的就是最多的元素。



```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        stack<int> st;
        for(int i = 0; i< nums.size(); i++){
            if(st.empty() || st.top() == nums[i]){
                st.push(nums[i]);
            } else {
                st.pop();
            }
        }
        return st.top();
        
    }
};
```

查看的时候这种方法应该类似于：Boyer-Moore Voting Algorithm，不过代码有更简单的实现。

```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        stack<int> st;
        int num = 0;
        int candidate;
        for(int i = 0; i< nums.size(); i++){
            if(num == 0){
                candidate = nums[i];
            }
            num += (nums[i] == candidate ? 1 : -1);
            
        }
        return candidate;
        
    }
};
```



其他的解法：

1. 排序，然后取nums[n/2]位置
2. hash记录，然后找到>n/2的元素
3. 暴力，遍历，然后累加，判断是否>n/2