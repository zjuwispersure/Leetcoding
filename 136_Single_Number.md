[题目介绍](https://leetcode.com/problems/single-number/)

Given a **non-empty** array of integers, every element appears *twice* except for one. Find that single one.

**Note:**

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

**Example 1:**

```
Input: [2,2,1]
Output: 1
```

**Example 2:**

```
Input: [4,1,2,1,2]
Output: 4
```



### 解法1

使用亦或操作，因为0^a = a,a^a = 0。这样最后剩余的就是多出来的数字。

```
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int result = 0;
        for(int num : nums){
            result ^= num;
        }
        return result;
        
    }
};
```

