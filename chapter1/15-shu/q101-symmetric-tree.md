# 101. Symmetric Tree

直达：https://leetcode.com/problems/symmetric-tree/description/

Given a binary tree, check whether it is a mirror of itself \(ie, symmetric around its center\).

For example, this binary tree`[1,2,2,3,4,4,3]`is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following`[1,2,2,null,3,null,3]`is not:

```
    1
   / \
  2   2
   \   \
   3    3
```

**Note:**  
Bonus points if you could solve it both recursively and iteratively.

## 分析

两棵树是对称的充要条件是第一棵树的左子树和第二棵树的右子树互相对称，并且第一棵树的右子树与第二棵树的左子树互相对称。

所以用一个判断两个数是否对称做辅助函数

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
    bool isSymmetric(TreeNode* root) {
        if(root==NULL) return true;
        return symmetricTrees(root->left, root->right);
    }
private:
    bool symmetricTrees(TreeNode* left, TreeNode* right){
        if(left==NULL && right==NULL) return true;
        if(left==NULL ^ right==NULL) return false;
        if(left->val != right->val) return false;
        if(!symmetricTrees(left->left, right->right)) return false;
        if(!symmetricTrees(left->right, right->left)) return false;
        return true;
    }
};
```



