# 82. Remove Duplicates from Sorted List II

直达：https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving onlydistinctnumbers from the original list.

For example,  
Given`1->2->3->3->4->4->5`, return`1->2->5`.  
Given`1->1->1->2->3`, return`2->3`.

## 分析

增加两个辅助指针，d\_head作为伪头节点，p\_haed辅助删除数据

需要注意的几个边界情况及解决方案

1. 头节点需要删除：设置伪头节点，伪头节点的下个元素是head，返回的时候返回d\_head的下一个节点
2. 最后一个节点需要删除：判断是否是最后一个节点，如果是的话将p指向空，返回结果

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
    ListNode* deleteDuplicates(ListNode* head) {
        if(head == NULL) return head;
        ListNode* d_head = new ListNode(0);
        ListNode* p_head = d_head;
        d_head -> next = head;
        while(head->next){
            if(head->val == head->next->val){
                int del_val = head->val;
                while(head->val == del_val){                   
                    if(head->next) head = head->next;
                    else{
                        p_head->next = NULL;
                        return d_head->next;
                    }
                }
                p_head->next = head;
            }else{
                p_head = head;
                head = head->next;
            }
        }
        return d_head->next;
    }
};
```



