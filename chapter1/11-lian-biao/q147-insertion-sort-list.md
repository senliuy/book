# 147. Insertion Sort List

直达：[https://leetcode.com/problems/insertion-sort-list/description/](https://leetcode.com/problems/insertion-sort-list/description/)

Sort a linked list using insertion sort.

## 分析

知识点在于链表的插入，分成两种情况。

1. 在头结点之前插入

如下图在3之前插入1：



![](/assets/14_1.png)



ListNode\* tmp = head;

head = head-&gt;next;

tmp-&gt;next = res;

res = tmp;

在中间或者尾部插入，如下图



![](/assets/147_3.png)



首先顺序遍历res链表，找到该插入的位置，即将head插入l2和l1之间

l2-&gt;next = tmp;

head = head-&gt;next;

tmp-&gt;next = l1;

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
    ListNode* insertionSortList(ListNode* head) {
        if(head==NULL || head->next==NULL) return head;
        ListNode* res = head;
        head = head->next;
        res->next = NULL;
        while(head){
            ListNode* tmp = head;
            if(head->val <= res->val){
                head = head->next;
                tmp->next = res;
                res = tmp;
            }else{
                ListNode* l1 = res;
                ListNode* l2 = l1;
                while(l1 && l1->val < head->val){
                    l2 = l1;
                    l1 = l1->next;
                }
                l2->next = tmp;
                head = head->next;
                tmp->next = l1;
            }
        }
        return res;
    }
};
```



