[题目介绍](https://leetcode.com/problems/maximal-square/)

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

**Example:**

```
Input: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```



### 解法

同最大正方形面积的题目，这里是正方形。



```
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
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
                    int length = min(j-lefti-1, height);
                    ret=max(length*length,ret);
                }
                lowi.push(j);
            }
        }
        return ret;   
    }
};
```

