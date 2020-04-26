# 环形链表 II

题目

```bash
给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。


示例 1：

输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。


示例 2：

输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。


示例 3：

输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。



进阶：
你是否可以不用额外空间解决此题？
```

题解

两种方法，一种比较容易想到的就是将各个节点加入一个哈希表，然后不断的对比哈希表中是否有元素相等，如果相等，那么该元素就会是这个环形链表的入口。另外一个不用额外空间的方法为双指针法，即快慢指针，但是需要分析清楚如何使用，在数学上可以画一下示意图了解下，当快慢指针第一次相遇后，将快指针放回头部，并按照慢速前进，此时二者再相遇的位置即为环形链表的入口，两种方法的代码如下。

```C++
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {//哈希表
public:
    ListNode *detectCycle(ListNode *head) {
        map<ListNode*, int> hashmap;
        ListNode *node = head;
        while(node!=NULL)
        {
            if(hashmap.count(node)==1) return node;
            else
            {
                hashmap[node]++;
                node = node->next;
            }
        }
        return NULL;
    }
};

class Solution {//双指针
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while(true)
        {
            if(fast==NULL||fast->next==NULL) return NULL;
            else
            {
                fast = fast->next->next;
                slow = slow->next;
                if(fast==slow) break;
            }
        }
        fast = head;
        while(slow!=fast)
        {
            fast = fast->next;
            slow = slow->next;
        }
        return fast;
    }
};
```
