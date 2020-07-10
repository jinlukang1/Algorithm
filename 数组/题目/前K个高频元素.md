# 前 K 个高频元素

题目

```bash
给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

 

示例 1:

输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
示例 2:

输入: nums = [1], k = 1
输出: [1]
 

提示：

你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
你的算法的时间复杂度必须优于 O(n log n) , n 是数组的大小。
题目数据保证答案唯一，换句话说，数组中前 k 个高频元素的集合是唯一的。
你可以按任意顺序返回答案。
```

题解

看到这个题目直接用python做了，因为题目本身是想让你实现一个topK的排序，可以痛堆排序进行实现，桶排序复杂度更低，但是实际上，这两种排序的方式不如python或者C++内置的排序方法，因为内置的方法是一种归并排序和插入排序的结合，在实际的速度上会更快一些。python的代码如下。

```py
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        res_dict = {}
        for num in nums:
            res_dict[num] = 0
        for num in nums:
            res_dict[num] += 1
        sorted_dict = sorted(res_dict.items(), key = lambda item: item[1], reverse = True)
        res = []
        for key in sorted_dict[:k]:
            res.append(key[0])
        return res
```

下面是一个topK的集合，代码如下。

```C++
方法一：使用STL排序算法对value进行排序  时间复杂度O(NlogN)

struct CmpByValue {
    bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) {
        return lhs.second > rhs.second; 
    }
};

vector<int> topKFrequent(vector<int>& nums, int k) {

    //统计次数 可以使用map 或 hash map
    map<int, int> m;
    //unordered_map<int, int> m;

    for (int i = 0; i < nums.size(); ++i)
    {
        ++m[nums.at(i)];
    }

    //根据value(统计次数)排序
    vector<pair<int, int> > v(m.begin(), m.end());
    
    //快速排序
    sort(v.begin(), v.end(), CmpByValue()); //从大到小

    //堆排序
    //std::make_heap(v.begin(), v.end(), CmpByValue());
    //std::sort_heap(v.begin(), v.end(), CmpByValue());

    //将前k个数值放入结果数组
    vector<int> k_frequent(k);
    for (int i = 0; i < k; ++i)
    {
        k_frequent.at(i) = v.at(i).first;
    }

    return k_frequent;
}


方法二：桶排序 时间复杂度O(N)
vector<int> topKFrequent(vector<int>& nums, int k) {

    //统计次数
    unordered_map<int, int> m;

    for (int i = 0; i < nums.size(); ++i)
    {
        ++m[nums.at(i)];
    }

    //使用二维数组  统计次数作为第一维（如果统计次数有相同，则将值追加到桶中）
    vector<vector<int>> buckets(nums.size() + 1);

    for (auto iter = m.begin(); iter != m.end(); ++iter)
    {
        buckets.at(iter->second).push_back(iter->first);
    }

    //将buckets中前k个高频元素放入res中
    vector<int> res(k);
    int count = 0;
    for (int i = buckets.size() - 1; i >= 0; --i)
    {
        for (int j = 0; j < buckets.at(i).size(); ++j)
        {
            res.at(count) = buckets.at(i).at(j);
            ++count;
            if (count == k)
                return res;
        }
    }

    return res;
}


方法三：使用STL 优先队列(堆) 最大堆 大小为N 时间复杂度O(N + KlogN)

struct CmpByValueLess {
    bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) {
        return lhs.second < rhs.second;
    }
};

vector<int> topKFrequent(vector<int>& nums, int k) {

    //统计次数
    unordered_map<int, int> m;

    for (int i = 0; i < nums.size(); ++i)
    {
        ++m[nums.at(i)];
    }

    //放入优先队列
    //注意：使用STL的优先队列 priority_queue  Comparator = greater 为小堆；Comparator = less 为大堆   
    priority_queue<pair<int, int>, vector<pair<int, int>>, CmpByValueLess> queue;
    for (auto iter = m.begin(); iter != m.end(); ++iter)
    {
        queue.push(*iter);
    }

    vector<int> res(k);
    for (int i = 0; i < k; ++i)
    {
        res.at(i) = queue.top().first;
        queue.pop();
    }

    return res;
}

方法四：使用STL 优先队列(堆) 最小堆 大小为K  时间复杂度O(KlogN)
vector<int> topKFrequent(vector<int>& nums, int k) {

    //统计次数
    //map<int, int> m;
    unordered_map<int, int> m; //<值，次数>

    for (int i = 0; i < nums.size(); ++i)
    {
        ++m[nums.at(i)];
    }

    //放入优先队列  注意：> 为小堆
    priority_queue<pair<int, int>, vector<pair<int, int>>, CmpByValue> heap;

    int count = 0;
    auto iter = m.begin();
    for (; iter != m.end(); ++iter)
    {
        if (count == k)
        {
            break;
        }

        heap.push(*iter);

        ++count;
    }

    //将大于堆顶的元素放入 并删除堆顶
    for (; iter != m.end(); ++iter)
    {
        if (iter->second > heap.top().second)
        {
            heap.pop();
            heap.push(*iter);
        }
    }

    vector<int> res(k);
    for (int i = 0; i < k; ++i)
    {
        res.at(i) = heap.top().first;
        heap.pop();
    }
    return res;
}
```