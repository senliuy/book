# 206. Reverse Linked List

直达：https://leetcode.com/problems/reverse-linked-list/description/

Reverse a singly linked list

## 分析

分成两种情况

1. 如果链表的节点数小于等于1个，直接返回链表即可
2. 如果大于1个，首先初始化几个指针用于遍历，如下图
   ```
   head  p
    |    |
    1 -> 2 -> 3 -> 4 -> 5
    |
    l
   ```

        然后判断什么时候到达链表尾部

        1.1 如果没有到达尾部

```
l = p->next;
p->next = head;
head = p;
p = l;
```

      1.2 如果到了尾部

```
p->next = head;
head = p;
return head;
```

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
    ListNode* reverseList(ListNode* head) {
        if(head == NULL || head->next==NULL) return head;
        ListNode* l = NULL;
        ListNode* p = head->next;
        head->next = NULL;
        while(p){
            if(p->next!=NULL){
                l = p->next;
                p->next = head;
                head = p;
                p = l;
            }else{
                p->next = head;
                head = p;
                return head;
            }
        }
    }
};
```



