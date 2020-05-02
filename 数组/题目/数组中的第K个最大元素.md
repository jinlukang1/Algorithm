# 数组中的第K个最大元素

题目

```bash
在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:

输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
示例 2:

输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。
```

题解

这个题的解法很多，总的来说，分为三种，在提交的过程中，我对比了这三种方法的效率，第一种方法是最简单的，先排序，然后找到第k个即可，这种方法的效率一定程度上比使用堆排序的方法还要快，因为C++中的sort()函数进行了很好的优化，是插入排序和归并排序的结合体，因此，效率还是比较高的。这个方法比较简单，这里就不贴代码了。还试了一下冒泡去前k个的方法，慢到爆炸。。

第二种方法是维护一个最小堆，遍历数组之后找到堆顶元素即可，总体来说，时间复杂度要比第一个方法直接排序要快低，但是实际表现差一点。下面提供两种不同方式的堆排序（调不同的库），效率差不多。代码如下。

```C++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        vector<int> result(k, INT_MIN);
        make_heap(result.begin(), result.end(), greater<int>());  
        for(int i=0; i<nums.size(); i++)
        {
            result.push_back(nums[i]);
            push_heap(result.begin(), result.end(), greater<int>());
            pop_heap(result.begin(), result.end(), greater<int>());
            result.pop_back();
        }
        // pop_heap(result.begin(), result.end());
        return result[0];
    }
};

class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<int>> p;
        for(int i=0; i<nums.size(); i++)
        {
            p.push(nums[i]);
            if(p.size()>k) p.pop();
        }
        return p.top();
    }
};
```

最后一种方法是利用了快速排序中的思想，将排序的过程中融合第k个，只排序和这k相关的那部分，效果也很好，只是过程中因为快排算法本身的问题，如果加入数组的随机再进行排序的话，效果会提升很多，代码如下。

```C++
class Solution {
public:
    int findKthLargest(vector<int>& v, int k) {
        srand(time(NULL));
        return findKthLargest(v, 0, v.size()-1, k);
    }
private:
    int findKthLargest(vector<int>& v, int l, int r, int k){

        int index = _partition(v, l, r);

        if( index+1 == k) return v[index];
        if( index+1 < k ) return findKthLargest(v, index+1, r, k );
        if( index+1 > k) return findKthLargest(v, l, index-1, k);

        return -1;
    }

    int _partition(vector<int>& v, int l, int r){

        int randIndex = rand()%(r-l+1)+l;
        swap(v[l], v[randIndex]);

        int e = v[l];

        int j = l, i = l+1;
        while(i <= r){
            if(v[i] >= e) swap(v[i], v[++j]);
            i++;
        }
        swap(v[l], v[j]);
        return j;
    }
};
```
