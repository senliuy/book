# 92. Reverse Linked List II

直达：[https://leetcode.com/problems/reverse-linked-list-ii/description/](https://leetcode.com/problems/reverse-linked-list-ii/description/)

Reverse a linked list from positionmton. Do it in-place and in one-pass.

For example:  
Given`1->2->3->4->5->NULL`, m = 2 and n = 4,

return`1->4->3->2->5->NULL`.

**Note:**  
Givenm,nsatisfy the following condition:  
1 ≤m≤n≤ length of list.

## 分析

题目要求一次遍历，且不能使用额外的存储空间。首先，设置一个伪头节点dhead（防止m=1）以及三个指针p1 = p2 =d\_head, p3 = head。开始从i=1开始遍历到n:

1. 当i&lt;m时，三个指针都向前移动一位
2. 当i=m是，p1停止遍历，此时p1后面就是要反转的链表，p2，p3继续遍历
3. 当i&gt;m且i&lt;=n时，此时需要交换节点，即把p3指向的节点插入到p1后面，如下图

![](/assets/Q92_1.png)

接下来就是链表节点的移动了

```
p2->next = p3->next;
p3->next = p1->next;
p1->next = p3;
```

移动后如下图

![](/assets/Q92_2.png)

由于不知道红色节点是否存在，所以需要判断p2-&gt;next用于决定p3的值

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
    ListNode* reverseBetween(ListNode* head, int m, int n) {
        ListNode* d_head = new ListNode(0);
        d_head -> next = head;
        ListNode* p1 = d_head;
        ListNode* p2 = d_head;
        ListNode* p3 = head;
        for(int i = 1; i<=n; i++){
            if(i < m){
                p1 = p1->next;
                p2 = p2->next;
                p3 = p3->next;
            }else if (i == m){
                p2 = p2->next;
                p3 = p3->next;
            }else{
                p2->next = p3->next;
                p3->next = p1->next;
                p1->next = p3;
                if(p2->next){
                    p3 = p2->next;
                }
            }
        }
        return d_head -> next;

    }
};
```



