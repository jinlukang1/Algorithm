# 搜索二维矩阵 II

题目

```bash
编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

每行的元素从左到右升序排列。
每列的元素从上到下升序排列。
示例:

现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。
```

题解

数组从右上角开始，向下的增加，向左是减少，根据这个原则，从右上角开始，我们不断的去减少列的值，增加行的值，可以遍历到我们的目标元素，时间复杂度大约为O(m+n)，代码如下。

```C++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        if(m==0) return false;
        int n = matrix[0].size();
        int col(n-1), row(0);
        while(col >= 0 && row <= m-1)
        {
            if(target<matrix[row][col]) col--;
            else if(target>matrix[row][col]) row++;
            else return true;
        }
        return false;
    }
};
```
