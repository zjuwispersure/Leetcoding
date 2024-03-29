[题目介绍](https://leetcode.com/problems/perfect-squares/)

Given a positive integer *n*, find the least number of perfect square numbers (for example, `1, 4, 9, 16, ...`) which sum to *n*.

**Example 1:**

```
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```

**Example 2:**

```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```



### 解法：DP



```
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n+1,0);
        for(int i=1;i<n+1;i++){
            dp[i] = INT_MAX;
        }
        for(int i = 1;i<=n;i++){
            for(int j =1; j*j <= i;j++){
                dp[i] = std::min(dp[i], dp[i-j*j] + 1);
            }
        }
        return dp[n];
    }
};
```

