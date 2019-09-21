[题目介绍](https://leetcode.com/problems/number-of-islands/)

Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
Input:
11110
11010
11000
00000

Output: 1
```

**Example 2:**

```
Input:
11000
11000
00100
00011

Output: 3
```



### 求解：DFS

思路是一致的，但是太不自信了。

对于每一个1，将其周围的1全部变为0，然后islandnum++。

```
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int islands = 0;
        for(int i = 0; i < grid.size(); i++){
            for(int j = 0; j < grid[0].size(); j++){
                if(grid[i][j] == '1'){
                    islands++;
                    wipe(grid,i,j);
                    
                }
            }
        }
        return islands;
    }
    void wipe(vector<vector<char>>& grid, int i, int j){
        if(i < 0 || i >= grid.size() || j < 0 || j >= grid[0].size() || grid[i][j] == '0'){
            return;
        }
        grid[i][j] = '0';
        wipe(grid, i-1, j);
        wipe(grid, i+1, j);
        wipe(grid, i, j-1);
        wipe(grid, i, j+1);
    }
};
```



### 解法：BFS

使用队列，四个方向依次进队列，处理完一个点以后继续处理

```
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int islands = 0;
        int offsets[] = {0,1,0,-1,0};
        for(int i = 0; i < grid.size(); i++){
            for(int j = 0; j < grid[0].size(); j++){
                if(grid[i][j] == '1'){
                    queue<pair<int, int>> bfp;
                    islands++;
                    grid[i][j] = '0';
                    bfp.push(make_pair(i,j));
                    while(!bfp.empty()){
                        pair<int, int> tmp = bfp.front();
                        bfp.pop();
                        for(int k = 0; k < 4; k++){
                            int row = tmp.first + offsets[k];
                            int col = tmp.second + offsets[k+1];
                            if(row >= 0 && row < grid.size() && col >= 0 && col < grid[0].size()  && grid[row][col] == '1'){
                                grid[row][col] = '0';
                                bfp.push(make_pair(row,col));
                            }
                        }
                    }
                }
            }
        }
        return islands;
    }
};
```

