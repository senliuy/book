# 114. Flatten Binary Tree to Linked List

直达：https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/

Given a binary tree, flatten it to a linked list in-place.

For example,  
Given

```
         1
        / \
       2   5
      / \   \
     3   4   6
```

The flattened tree should look like:

```
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
```

## 分析

如上图，首先将左右子树flatten，然后再转换成程序的输出。同样，左右子树也可以通过这个方法进行flat。如下图所示。所以，该题可以通过递归进行计算。转换方式是将左子树设成根节点的右子树，将右子树接到原左子树的叶节点的地方。

```
  1
 / \
2   5
 \   \
  3   6
   \
    4  
```

## C++代码

```cpp
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
    void flatten(TreeNode* root) {
        if(!root || !root->left && !root->right) return;
        flatten(root->left);
        flatten(root->right);
        TreeNode* temp_right = root->right;
        root->right = root->left;
        root->left = NULL;
        while(root->right) root = root->right;
        root->right = temp_right;
    }
};
```



