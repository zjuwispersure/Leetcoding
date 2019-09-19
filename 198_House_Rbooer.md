[题目介绍](https://leetcode.com/problems/house-robber/)

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```





### 解法：DP

动态规划，对于某个点i，最大取值为max(nums[i] + dp[i-2], dp[i-1]).

```
class Solution {
public:
    int rob(vector<int>& nums) {
        int dp[nums.size()+2] = {0};
        
        for(int i = 0; i < nums.size(); i++){
            dp[i+2] = max(dp[i] + nums[i], dp[i+1]);
        }
        return dp[nums.size()+1];
        
    }
};
```



可以精简下，不用数组，改用三个变量来处理。

```
class Solution {
public:
    int rob(vector<int>& nums) {
        int prev2 = 0;
        int prev1 = 0;
        int now = 0;
        
        for(int i = 0; i < nums.size(); i++){
            now = max(prev2 + nums[i], prev1);
            prev2 = prev1;
            prev1 = now;
        }
        return now;
        
    }
};
```

