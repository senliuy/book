# 109. Convert Sorted List to Binary Search Tree

直达：[https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/description/](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/description/)

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees ofeverynode never differ by more than 1.

**Example:**

```
Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

## 分析

和Q108一样，重点是如何确定链表中间元素以及如何切割链表。

用两个指针遍历，快指针fast每次走两步，慢指针slow每次走一步，当快指针走到结尾处（或者倒数第二个）尾指针正好走到中间（或者左偏一格），则slow的下一个便是中间指针，如下图。

```
     slow  fast
      |     |
-10, -3, 0, 5, 9
 |        |
head     mid
```

将mid作为根节点，head到slow作为左子树链表，mid-&gt;next到最后作为右子树的链表，迭代进行直到链表为空或者只剩一个元素的时候返回即可。

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
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* sortedListToBST(ListNode* head) {
        if (!head) return NULL;
        if (!head->next) return new TreeNode(head->val);
        ListNode* slow = head;
        ListNode* fast = head->next;
        while(fast->next && fast->next->next){
            fast = fast->next->next;
            slow = slow->next;
        }
        ListNode* mid = slow->next;
        TreeNode* root = new TreeNode(mid->val);
        l1->next = NULL;
        root->left = sortedListToBST(head);
        root->right = sortedListToBST(mid->next);
        return root;
    }
};
```



