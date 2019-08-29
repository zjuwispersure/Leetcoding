[题目介绍](https://leetcode.com/problems/largest-rectangle-in-histogram/)

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![image](img/84.png)


## 方法1:暴力统计

1、统计所有的高度

2、对于某个高度h，遍历不小于该高度的连续柱子数量为n，则面积为h*n,与最大面积比较并赋值

3、返回最大面积。

代码如下：时间复杂度O(n^2),空间复杂度O(n)

```c++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        set<int> heightSize;
        for(int i = 0; i< heights.size();i++){
            heightSize.insert(heights[i]);
        }
        int result = 0;
        for(set<int>::iterator it = heightSize.begin(); it != heightSize.end(); it++){
            int height = *it;
            int width = 0;
            for(int i = 0; i< heights.size(); i++){
                if(heights[i] >= height){
                    width++;
                } else {
                    result = std::max(result, width * height);
                    width = 0;
                }
            }
            result = std::max(result, width * height);
        }
        return result;
        
    }
};
```



## 方法2:单调栈

参考大神的思路，使用[单调递增栈](https://github.com/zjuwispersure/Leetcoding/blob/master/MonotoneStack.md)。

使用单调递增栈，遍历heights，

+ 如果heights[i]大于栈顶元素，符合单调递增栈的定义，入栈即可；

+ 如果heights[i]小于栈顶元素，则栈顶元素出栈，并计算面积，并更新最大面积；依次比较直到heights[i]大于栈顶元素，入栈。

  有个trick是在最后添加一个0，这样最后可以将栈中所有元素都出栈来做比较。

比较形象的是想象一个递增的阶梯，对于不满足递增关系的部分，则用不满足部分的面积来与最大面积做比较；



```C++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> indexs;
        int maxArea = 0;
        heights.push_back(0);
        for(int i = 0; i < heights.size(); i++){
            while(!indexs.empty() && heights[indexs.top()] > heights[i]){
                int h = heights[indexs.top()];
                indexs.pop();
                int index = indexs.empty()? -1:indexs.top();
                maxArea = std::max(maxArea, h *(i - index - 1));
                
            }
            indexs.push(i);
        }
        return maxArea;
        
    }
};
```





