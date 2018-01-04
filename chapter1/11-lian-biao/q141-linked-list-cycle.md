# 141. Linked List Cycle

直达：https://leetcode.com/problems/linked-list-cycle/description/

Given a linked list, determine if it has a cycle in it.

Follow up:  
Can you solve it without using extra space?

## 分析

设置两个指针，快指针每次遍历两个节点，慢指针每次遍历一个节点，如果快指针能和慢指针相遇，则说明存在环。

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
    bool hasCycle(ListNode *head) {
        if(!head) return false;
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast && fast->next){
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow) return true;
        }
        return false;
    }
};
```



