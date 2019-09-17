[题目介绍](https://leetcode.com/problems/maximum-product-subarray/)

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

**Example 1:**

```
Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**

```
Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```



### 解法：暴力

两个for循环轮询。

```
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int result = INT_MIN;
        for(int i=0; i < nums.size(); i++){
            int tmp = 1;
            for(int j=i; j<nums.size(); j++){
                tmp *= nums[j];
                if(tmp > result){
                    result = tmp;
                }
            }
        }
        
        return result;
    }
};
```





### 解法：DP

保存最大值和最小值，依次比较x、x*max、x*min 三者。每次都要有x，否则就是不连续了。

```
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        if (nums.empty()) return 0;
        int res = nums[0], mn = nums[0], mx = nums[0];
        for (int i = 1; i < nums.size(); ++i) {
            int tmax = mx, tmin = mn;
            mx = max(max(nums[i], tmax * nums[i]), tmin * nums[i]);
            mn = min(min(nums[i], tmax * nums[i]), tmin * nums[i]);
            res = max(res, mx);
        }
        return res;
    }
};
```



