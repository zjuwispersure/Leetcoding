[题目介绍](https://leetcode.com/problems/product-of-array-except-self/)

Given an array `nums` of *n* integers where *n* > 1,  return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

**Example:**

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

**Note:** Please solve it **without division** and in O(*n*).

**Follow up:**
Could you solve it with constant space complexity? (The output array **does not** count as extra space for the purpose of space complexity analysis.)



### 解法

尝试了除法，暴力遍历，除法因为可能存在多个0，没发搞起；暴力的话超时。

准备两个vector，分别记录前后累积的乘积。这里的空间复杂度是$O(n)$.

```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        vector<int> result(nums.size(),1);
        vector<int> front(nums.size(),1);
        vector<int> back(nums.size(),1);
        
        for(int i=1;i<nums.size();i++){
            front[i] = front[i-1]*nums[i-1];
        }
        for(int i=nums.size()-2;i>=0;i--){
            back[i] = back[i+1]*nums[i+1];
        }
        for(int i= 0; i<nums.size();i++){
            result[i] = front[i]* back[i];
        }
        return result;
        
    }
};
```



将数组转换为两个变量来代替。

```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int size = nums.size();
        vector<int> result(size,1);
        int front=1;
        int back=1;
        
        for(int i= 0; i<size;i++){
            result[i] *= front;
            front *= nums[1];
            result[size-i-1] *= back;
            back *= nums[n-i-1];
        }
        return result;
        
    }
};
```

