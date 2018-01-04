# 142. Linked List Cycle II

直达：[https://leetcode.com/problems/linked-list-cycle-ii/description/](https://leetcode.com/problems/linked-list-cycle-ii/description/)

Given a linked list, return the node where the cycle begins. If there is no cycle, return`null`.

**Note:**Do not modify the linked list.

**Follow up**:  
Can you solve it without using extra space?

## 分析

设置三个指针，快指针fast每次遍历两个节点，慢指针slow1，slow2每次遍历两个节点。

开始的时候fast和slow1先从头节点开始遍历，相遇的时候fast走的距离是slow1的两倍，如下图:

![](/assets/Q142_1.png)

假设非环链表部分的长度是x，环的周长是y，fast和slow1在d处相遇，此时fast比slow1多走了一个圆环，于是有

2 \* \(x+d\) = x+d+y

化简得：

x = y-d

第二轮遍历的时候slow2从头结点开始遍历，slow1从d处开始遍历，当遍历到环起始点的时候，因为x=y-d，所以两指针会在这个地方相遇。

## C++代码

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if(!head) return NULL;
        ListNode* slow1 = head;
        ListNode* slow2 = head;
        ListNode* fast = head;
        while(fast && fast->next){
            fast = fast->next->next;
            slow1 = slow1->next;
            if(fast == slow1){
                while(slow2 != slow1){
                    slow2 = slow2->next;
                    slow1 = slow1->next;
                }
                return slow2;
            }
        }
        return NULL;
    }
};
```



