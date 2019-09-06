[题目介绍](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

**Example 2:**

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```



### 解法

从头开始找到最小的数值min，然后依次比较当前值与min的delta，更新delta。

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int result = INT_MIN;
        int min = INT_MAX;
        for(int i = 0; i < prices.size(); i++){
            int value = prices[i];
            if(min > value){
                min = value;
            }
            if(result < value - min){
                result = value - min;
            }
        }
        if(result < 0){
            result = 0;
        }
        return result;
    }
};
```



用一下系统函数来优化下代码逻辑。

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int result = 0;
        int min_value = INT_MAX;
        for(int i = 0; i < prices.size(); i++){
            int value = prices[i];
            min_value = min(min_value, prices[i]);
            result = max(result, prices[i] - min_value);
            
        }
       
        return result;
    }
};
```

