[题目介绍](https://leetcode.com/problems/longest-consecutive-sequence/)

百思不得其解，参考其让人的答案后搞定。

主要是引入了unsorted_set，该容器的查找、删除都是常数时间。

将数组存入unsorted_set，遍历数组num：

1. unsorted_set删除num
2. num_left--查找；num_right++查找
3. 比较最大的连续值



```
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> record(nums.begin(), nums.end());
        int r = 0;
        for(int n : nums){
            if(record.find(n) == record.end()) {
                continue;
            }
            record.erase(n);
            int left = n - 1;
            int right = n + 1;
              while(record.find(left) != record.end()){
                record.erase(left);
                left--;
            }
            while(record.find(right) != record.end()){
                record.erase(right);
                right++;
            }
            r = max(r, right - left - 1);
        }
        return r;
        
        
    }
};
```

