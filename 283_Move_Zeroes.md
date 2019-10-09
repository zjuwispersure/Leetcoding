[题目介绍](https://leetcode.com/problems/move-zeroes/)



Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note**:

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.



### 解法

快慢指针，慢指针指示非0，快指针指示当前位置。从头开始遍历，遇到非0的则将慢指针赋值，保证非0的顺序，后面的补0；

```
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int nonZeroPosition = 0;
        for(int i =0;i<nums.size();i++){
            if(nums[i]!=0){
                nums[nonZeroPosition++] = nums[i];
            }
        }
        for(int i=nonZeroPosition;i<nums.size();i++){
            nums[i] = 0;
        }
        
    }
};
```



快慢指针如果非0值在数组尾部，则耗时较大，针对此情况进行适当优化。从头开始遍历，遇到非0的则进行交换；

```
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for(int nonZeroPosition=0,cur=0;cur<nums.size();cur++){
            if(nums[cur]!=0){
                swap(nums[nonZeroPosition++], nums[cur]);
            }
        }
        
    }
};
```

