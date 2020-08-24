# 摆动排序 II

题目

```bash
给定一个无序的数组 nums，将它重新排列成 nums[0] < nums[1] > nums[2] < nums[3]... 的顺序。

示例 1:

输入: nums = [1, 5, 1, 1, 6, 4]
输出: 一个可能的答案是 [1, 4, 1, 5, 1, 6]
示例 2:

输入: nums = [1, 3, 2, 2, 3, 1]
输出: 一个可能的答案是 [2, 3, 1, 3, 1, 2]
说明:
你可以假设所有输入都会得到有效的结果。

进阶:
你能用 O(n) 时间复杂度和 / 或原地 O(1) 额外空间来实现吗？
```

题解

比较简单的思路是直接逆向排序然后再插着排序，另外的一种方法是使用快速排序的思路来做，代码如下。

```python
# 直接排序的思路
class Solution:
    def wiggleSort(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        nums.sort(reverse=True)
        mid = len(nums) // 2
        nums[1::2],nums[0::2] = nums[:mid], nums[mid:]

# 快速排序思路
class Solution:
    def wiggleSort(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        if n < 2:return nums
        mid = (0 + n-1) // 2 # 中位数索引
        

        # 快速排序中的一次划分
        def partition(begin,end):
            left,right = begin,end
            while left < right:
                while left < right and nums[left] < nums[right]:right -= 1
                if left < right:
                    nums[left],nums[right] = nums[right],nums[left]
                    left += 1
                while left < right and nums[left] < nums[right]: left += 1
                if left < right:
                    nums[left],nums[right] = nums[right],nums[left]
                    right -= 1
            return left

        # 找到中位数对应的数值
        left,right = 0, n-1
        while True:
            pivot = partition(left,right)
            if pivot == mid:break
            elif pivot > mid:right = pivot - 1
            else:left = pivot + 1

        # 三路划分(荷兰旗)
        midNum = nums[mid]
        left,curr,right = 0, 0, n-1
        while curr < right:
            if nums[curr] < midNum:
                nums[left],nums[curr] = nums[curr],nums[left]
                left += 1
                curr += 1
            elif nums[curr] > midNum:
                nums[curr],nums[right] = nums[right],nums[curr]
                right -= 1
            else:
                curr += 1

        # 交叉合并
        small,big ,_nums = mid,n-1,nums[:]
        for i in range(n):
            if i%2 == 0:
                nums[i] = _nums[small]
                small -= 1
            else:#big
                nums[i] = _nums[big]
                big -= 1
```