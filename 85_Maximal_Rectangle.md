## [题目介绍](https://leetcode.com/problems/maximal-rectangle/)

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

Example

```
Input:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
Output: 6
```





## 解法

参考[Largest Rectangle in Histogram](https://github.com/zjuwispersure/Leetcoding/blob/master/84_Largest_Rectangel_in_Histogram.md) 的求解方法，将2D的内容从上到下拼接出histogram，histogram的高度由每一层及其上面连续的1组成。

```C++
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        if(matrix.empty()|| matrix[0].empty())
            return 0;
        int rows=matrix.size();
        int cols=matrix[0].size();
        int ret=0;
        vector<int> h(cols+1);
        for(int i=0;i<rows;i++) {
            stack<int> lowi;
            for(int j=0;j<=cols;j++) {
                h[j]=((j!=cols && matrix[i][j]=='1')?h[j]+1:0);
                while(!lowi.empty() && (h[j]<h[lowi.top()])){
                    int height=h[lowi.top()];
                    lowi.pop();
                    int lefti=(lowi.empty()?-1:lowi.top());
                    ret=max((j-lefti-1)*height,ret);
                }
                lowi.push(j);
            }
        }
        return ret;     
    }
};
```

