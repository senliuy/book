2. Add Two Numbers

直达：https://leetcode.com/problems/add-two-numbers/description/

You are given two**non-empty**linked lists representing two non-negative integers. The digits are stored in**reverse order**and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## 分析

两链表求和，重点是保存进位标识（carry），每遍历一次就新建一个节点并将新节点插入到结果链表中。

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int flag = 0; //表示进位
        ListNode res(0);
        ListNode *p = &res;
        ListNode *p_head = p;
        while(l1 || l2 || flag){
            int sum = (l1?l1->val:0) + (l2?l2->val:0) + flag;
            flag = sum/10;
            p->next = new ListNode(sum%10);
            p = p->next;
            l1 = l1?l1->next:l1;
            l2 = l2?l2->next:l2;
        }
        return p_head->next;
    }
};
```



