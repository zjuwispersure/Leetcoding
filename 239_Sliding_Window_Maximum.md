[题目介绍](https://leetcode.com/problems/sliding-window-maximum/)

Given an array *nums*, there is a sliding window of size *k* which is moving from the very left of the array to the very right. You can only see the *k* numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

**Example:**

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**Note:**
You may assume *k* is always valid, 1 ≤ k ≤ input array's size for non-empty array.

**Follow up:**
Could you solve it in linear time?



### 解法

使用双向队列deque。队列中保持的状态是：当前队列的队尾元素要大于入队的元素。新的元素必须要入队列。

超过k个元素时，将队列的front加入result。

```
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int size = nums.size();
        deque<int> dp;
        vector<int> result;
        for(int i =0;i<size; i++){
            if(!dp.empty() && dp.front() == i-k){
                dp.pop_front();
            }
            while(!dp.empty() && nums[dp.back()]<nums[i]){
                dp.pop_back();
            }
            dp.push_back(i);
            if(i>=k-1){
                result.push_back(nums[dp.front()]);
            }
        }
        return result;
    }
};
```

