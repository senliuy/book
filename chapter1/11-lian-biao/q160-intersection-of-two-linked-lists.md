# 160. Intersection of Two Linked Lists

直达：https://leetcode.com/problems/intersection-of-two-linked-lists/description/

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```

begin to intersect at node c1.

**Notes:**

* If the two linked lists have no intersection at all, return`null`
* The linked lists must retain their original structure after the function returns.
* You may assume there are no cycles anywhere in the entire linked structure.
* Your code should preferably run in O\(n\) time and use only O\(1\) memory.

# 分析

有限次数遍历的复杂度仍旧是O\(n\).

1. 遍历两个数组的长度;
2. 长数组比短数组长的部分一定不可能是交点，可先遍历长数组，知道剩下的长度等于短数组；
3. 同事遍历两个数组并比较是否是交点。

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (headA==NULL || headB==NULL) return NULL;
        int lenA = 0, lenB = 0;
        ListNode* lA = headA;
        ListNode* lB = headB;
        while(lA){
            lA = lA->next;
            lenA++;
        }
        while(lB){
            lB = lB->next;
            lenB++;
        }
        lA = headA; lB = headB;
        if(lenA > lenB){
            for(int i = 0; i<lenA-lenB; i++) lA = lA->next;
        }else{
            for(int i = 0; i<lenB-lenA; i++) lB = lB->next;
        }
        while(lA != lB){
            lA = lA->next;
            lB = lB->next;
        }
        return lA;
    }
};
```



