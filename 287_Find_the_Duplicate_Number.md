[题目介绍](https://leetcode.com/problems/find-the-duplicate-number/)

Given an array *nums* containing *n* + 1 integers where each integer is between 1 and *n* (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

**Example 1:**

```
Input: [1,3,4,2,2]
Output: 2
```

**Example 2:**

```
Input: [3,1,3,4,2]
Output: 3
```

**Note:**

1. You **must not** modify the array (assume the array is read only).
2. You must use only constant, *O*(1) extra space.
3. Your runtime complexity should be less than *O*(*n*2).
4. There is only one duplicate number in the array, but it could be repeated more than once.



### 解法：set

用set来记录，如果遍历过程中发现set中已经记录，则说明该数字是重复的。

这里中间return的话在leetcode中会报错，因此最后还是要添加一个return语句。

```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        std::set<int> s;
        for(int i=0; i<nums.size();i++){
            if(s.count(nums[i]) != 0){
                return nums[i];
            }
            s.insert(nums[i]);
        }
        return 0;
    }
};
```



### 解法：排序

排序，然后前后比较，有相同的则是重复数字，因为输入都是1～n的数字，因此pre初始化为0即可。

```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int pre = 0;
        for(int i=0; i<nums.size();i++){
            if(pre == nums[i]){
                return nums[i];
            }
            pre = nums[i];
        }
        return 0;
    }
};
```





### 解法：环检测

提示中的方法，转变为环的问题，然后利用环检测算法去解决。多加强着方便的锻炼，很精妙。

```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
         int tortoise = nums[0];
        int hare = nums[0];
        do {
            tortoise = nums[tortoise];
            hare = nums[nums[hare]];
        } while (tortoise != hare);

        // Find the "entrance" to the cycle.
        int ptr1 = nums[0];
        int ptr2 = tortoise;
        while (ptr1 != ptr2) {
            ptr1 = nums[ptr1];
            ptr2 = nums[ptr2];
        }

        return ptr1;
    }
};
```

