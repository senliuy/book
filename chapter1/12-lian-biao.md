# 86. Partition List

# 问题

直达: https://leetcode.com/problems/partition-list/description/

Given a linked list and a valuex, partition it such that all nodes less thanxcome before nodes greater than or equal tox.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,  
Given`1->4->3->2->5->2`andx= 3,  
return`1->2->2->4->3->5`.

给定一个整数链表和一个整数x，将小于x的移到新链表的左边，大于等于的移到右边，保证链表的同一部分的顺序不变，如上图。

# 分析

初始化两个链表，一个保存小于x的，一个保存大于等于x的，最后重新连接两个链表即可。

```cpp
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        ListNode* l1 = new ListNode(0);
        ListNode* l2 = new ListNode(0);
        ListNode* l1_2 = l1;
        ListNode* l2_2 = l2;
        while(head){
            if(head->val >= x){
                l2_2 -> next = head;
                l2_2 = l2_2->next;
            }else{
                l1_2 ->next = head;
                l1_2 = l1_2->next;
            }
            head = head->next;
        }
        l2_2->next = NULL;
        l1_2->next = l2->next;
        return l1->next;
    }
};
```



