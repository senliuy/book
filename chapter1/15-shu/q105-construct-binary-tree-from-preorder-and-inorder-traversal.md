# 105. Construct Binary Tree from Preorder and Inorder Traversal

直达：[https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)

Given preorder and inorder traversal of a tree, construct the binary tree.

## 分析

对于先序遍历和中序遍历的两串字符串，先序遍历的第一个字符便是当前树的根节点。为了迭代的使用该算法，需要确定左右两棵子树的先序遍历和中序遍历序列。

对于中序遍历，从当前字符串中找到先序遍历序列的第一个字符，当前字符左侧便为左子树的中序遍历序列（假设有m个字符），右侧便是右子树的中序遍历序列。

对于先序遍历，从第一个元素开始的m个元素是左子树的先序遍历，剩下的便是右子树的先序遍历。

为了节约存储空间，可以构建全局变量的hash表存储树节点在中序遍历序列中的位置。

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
    unordered_map<int, int> hash;
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if(preorder.empty()) return NULL;
        for(int i = 0; i < inorder.size(); i++) hash[inorder[i]] = i;
        return helper(preorder, inorder, 0, preorder.size() - 1, 0, inorder.size() - 1);
    }
private:
    TreeNode* helper(vector<int>& preorder, vector<int>& inorder, int s0, int e0, int s1, int e1){
        if(s0 > e0 || s1 > e1) return NULL;
        int mid = hash[preorder[s0]];
        TreeNode* root = new TreeNode(preorder[s0]);
        int num = mid-s1;
        root->left = helper(preorder, inorder, s0+1, s0+num, s1, mid-1);
        root->right = helper(preorder, inorder, s0+num+1, e0, mid+1, e1);
        return root;
    }
};
```



