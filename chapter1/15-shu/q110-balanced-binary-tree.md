# 110. Balanced Binary Tree

直达：[https://leetcode.com/problems/balanced-binary-tree/description/](https://leetcode.com/problems/balanced-binary-tree/description/)

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees ofeverynode never differ by more than 1.

## 分析

平衡二叉树的两棵子树的高度差小于2且左右两棵子树都是平衡二叉树，递归的判断即可。另外，树的高度也可以通过递归进行计算。

## C++代码：

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
    bool isBalanced(TreeNode* root) {
        if(!root) return true;
        if(abs(treeHeight(root->left) - treeHeight(root->right)) >= 2) return false;
        return isBalanced(root->left) && isBalanced(root->right);
    }
private:
    int treeHeight(TreeNode* root){
        if (!root) return 0;
        return max(treeHeight(root->left), treeHeight(root->right))+1;
    }
};
```



