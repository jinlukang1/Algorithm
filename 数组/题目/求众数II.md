# 求众数 II

题目（多数元素的进阶版）

```bash
给定一个大小为 n 的数组，找出其中所有出现超过 ⌊ n/3 ⌋ 次的元素。

说明: 要求算法的时间复杂度为 O(n)，空间复杂度为 O(1)。

示例 1:

输入: [3,2,3]
输出: [3]
示例 2:

输入: [1,1,1,3,3,2,2,2]
输出: [1,2]
```

摩尔投票法

核心就一句话，每次都拿走3个不一样的数, 那么最后剩下的, 一定是A和B，代码如下，是多数元素的进阶版。

```C++
/*
时间复杂度为：O(n)
空间复杂度为：O(1)
*/
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int len = nums.size();
        vector<int>res, cands, cnts;
        if(len == 0){//没有元素，直接返回空数组
            return res;
        }
        cands.assign(2, nums[0]);
        cnts.assign(2, 0);
        //第1阶段 成对抵销
        for(auto num: nums){
            bool flag = false;
            for(int i = 0; i < cands.size(); ++i){
                if(num == cands[i]){
                    ++cnts[i];
                    flag = true;
                    break;
                }
            }
            if(!flag){
                bool flag2 = false;
                for(int j = 0; j < cands.size(); ++j){
                    if(cnts[j] == 0){
                        flag2 = true;
                        cands[j] = num;
                        cnts[j]++;
                    }
                }
                if(!flag2){
                    for(int j = 0; j < cnts.size(); ++j){
                        --cnts[j];
                    }
                }
            }
        }

        //第2阶段 计数 数目要超过三分之一
        cnts[0] = cnts[1] = 0;
        if(cands[0] == cands[1])
            cands.pop_back();
        for(auto num:nums){
            for(int i = 0; i < cands.size(); ++i){
                if(cands[i] == num){
                    ++cnts[i];
                    break;
                }
            }
        }
        for(int i = 0; i < cands.size(); ++i){
            if(cnts[i] > len / 3){
                res.push_back(cands[i]);
            }
        }
        return res;
    }
};
```