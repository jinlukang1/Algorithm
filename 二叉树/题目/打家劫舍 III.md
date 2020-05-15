# 打家劫舍 III

题目

```bash
在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

示例 1:

输入: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
示例 2:

输入: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

输出: 9
解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.
```

题解

参考之前的打家劫舍的题目，可以想到用动态规划的方法，但是由于树结构天生比较适合用递归去解，因此，我们可以使用递归去解这个题目，首先可以想到的就是完全递归的方法。代码如下。

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int rob(TreeNode* root) {
        if(root==nullptr) return 0;
        int money = root->val;
        if(root->left!=nullptr)
        {
            money += rob(root->left->left) + rob(root->left->right); 
        }
        if(root->right!=nullptr)
        {
            money += rob(root->right->left) + rob(root->right->right);
        }
        return max(money, rob(root->left)+rob(root->right));
    }
};
```

但是上面的方法明显有一些问题，就是会超时，因为对于递归来说，会涉及到子结构的重复计算，因此，我们考虑使用一个哈希表来存储每一个节点的值，对于这个节点，如果这个值之前已经计算过，那么我们可以直接取出这个值进行计算，具体的代码如下。这里要注意的就是，C++里面对于这个hashmap你需要在函数里面指向这个变量的地址才能将对应的值存储进去，或者用全局变量也可以。

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int rob(TreeNode* root) {
        unordered_map<TreeNode*, int> memo;
        return rob_memo(root, memo);
    }
    int rob_memo(TreeNode* root, unordered_map<TreeNode*, int> &memo)
    {
        if(root==nullptr) return 0;
        // cout << memo.count(root) << endl;
        if(memo.count(root)==1){
            // cout << "get " << memo[root] << " !";
            return memo[root];
            }
        int money = root->val;
        if(root->left!=nullptr)
        {
            money += rob_memo(root->left->left, memo) + rob_memo(root->left->right, memo); 
        }
        if(root->right!=nullptr)
        {
            money += rob_memo(root->right->left, memo) + rob_memo(root->right->right, memo);
        }
        int result = max(money, rob_memo(root->left, memo)+rob_memo(root->right, memo));
        memo[root] = result;
        return result;
    }
};
```
