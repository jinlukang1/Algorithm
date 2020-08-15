# x 的平方根

题目

```bash
实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

示例 1:

输入: 4
输出: 2
示例 2:

输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
```

题解

使用二分搜索，注意边界条件等，代码如下。

```C++
class Solution {
public:
    int mySqrt(int x) {
        long left(0), right(x/2+1);
        while(left<=right)
        {
            long mid = left + (right - left) / 2;
            long square = mid * mid;
            if(square<x) left = mid + 1;
            else if(square>x) right = mid - 1;
            else return (int) mid;
        }
        return (int) left - 1;
    }
};
```

二分法的模板

