# 106. Construct Binary Tree from Inorder and Postorder Traversal

直达：[https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)

Given inorder and postorder traversal of a tree, construct the binary tree.

## 分析

和Q105思想相同。

需要注意的是根节点是后序遍历序列的最后一个元素。

左，右子树的中序和Q105取法相同。

左子树的后续遍历是开始到m-1个字符，右子树的后序遍历是m到倒数第二个字符

C++代码：

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
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if(inorder.empty()) return NULL;
        for(int i = 0; i < inorder.size(); i++) hash[inorder[i]] = i;
        return helper(inorder, postorder, 0, inorder.size() - 1, 0, postorder.size() - 1);
    }
private:
    TreeNode* helper(vector<int>& inorder, vector<int>& postorder, int s0, int e0, int s1, int e1){
        if(s0 > e0 || s1 > e1) return NULL;
        int mid = hash[postorder[e1]];
        TreeNode* root = new TreeNode(postorder[e1]);
        int num = mid-s0;
        root->left = helper(inorder, postorder, s0, mid-1, s1, s1+num-1);
        root->right = helper(inorder, postorder, mid+1, e0, s1+num, e1-1);
        return root;
    }
};
```



