# 19. Remove Nth Node From End of List

直达：https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/

Given a linked list, remove thenthnode from the end of list and return its head.

For example,

```
Given linked list: 1->2->3->4->5, and n = 2.
After removing the second node from the end, the linked list becomes 
1->2->3->5.
```

**Note:**  
Given n will always be valid. Try to do this in one pass.

## 分析

两个指针p, end，end走了n步之后p再开始走，另外还需要一个prior指针跟在p的前面，以便用处链表节点的删除。

重点在于边界情况的处理，即n等于链表的长度。

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* p = head;
        ListNode* end = head;
        ListNode* prior = head;
        int cnt = 0;
        while(end -> next){
            if(cnt >= n-1){
                end = end -> next;
                prior = p;
                p = p -> next;
                cnt++;
            }else{
                end = end -> next;
            }
            cnt++;
        }
        if(p == prior){
            head = head -> next;
        }else{
            prior -> next = p ->next;
        }
        return head;
    }
};
```



