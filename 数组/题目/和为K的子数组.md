# 和为K的子数组

题目

```bash
给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。

示例 1 :

输入:nums = [1,1,1], k = 2
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
说明 :

数组的长度为 [1, 20,000]。
数组中元素的范围是 [-1000, 1000] ，且整数 k 的范围是 [-1e7, 1e7]。
```

题解

主要是两种方法，一种是基于暴力方法的优化，时间复杂度O(n2)，另一种是基于hash表+前缀和数字的方式，时间复杂度O(n)。

基于暴力方法的优化，相当于在循环过程中省去每一步需要的多余计算，很容易理解，代码如下。

```C++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int res(0), n(nums.size());
        for(int left = 0; left < n; left++)
        {
            int sum = 0;
            for(int right = left; right<n; right++)
            {
                sum += nums[right];
                if(sum == k) res++;
            }
        }
        return res;
    }
};
```

基于hash表+前缀和的方法，主要思路如下，从前往后循环，首先计算到当前元素为止的前缀和，然后计算该前缀和与k的差值，在hash表中查询是否存在有前缀和为该差值的值，结果直接可以加上这个值（也就是次数），最后循环结束之后得到的就是该题目的结果。利用hash表，是空间换时间的一个常见操作。

```C++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        unordered_map<int, int> hashmap;
        hashmap[0] = 1;
        int count(0), sum(0);
        for(int i=0; i<nums.size(); i++)
        {
            sum += nums[i];
            if(hashmap.count(sum-k) != 0) count += hashmap[sum-k];
            hashmap[sum]++;
        }
        return count;
    }
};
```
