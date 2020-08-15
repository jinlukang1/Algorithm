# Excel表列序号

题目

```bash
给定一个Excel表格中的列名称，返回其相应的列序号。

例如，

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
示例 1:

输入: "A"
输出: 1
示例 2:

输入: "AB"
输出: 28
示例 3:

输入: "ZY"
输出: 701
```

题解

按照数学思路模式来即可，中间需要注意取数方式为`s[i] - 'A' + 1`，代码如下。

```C++
class Solution {
public:
    int titleToNumber(string s) {
        int res = 0;
        for(int i=0; i<s.size(); i++)
        {
            res += (s[i] - 'A' + 1) * (pow(26, (s.size() - i - 1)));
        }
        return res;
    }
};
```
