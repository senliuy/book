# 144. Binary Tree Preorder Traversal

直达：https://leetcode.com/problems/binary-tree-preorder-traversal/

Given a binary tree, return thepreordertraversal of its nodes' values.

For example: Given binary tree\[1,null,2,3\],

```
1
 \
  2
 /
3
```

return\[1,2,3\].

**Note**:Recursive solution is trivial, could you do it iteratively?

## 分析

用递归解决二叉树的遍历是非常普遍的解法，题目提出能否使用迭代来进行二叉树的先序遍历。

对于先序遍历，需要使用堆栈做辅助。首先树顶入栈，然后执行while循环直到堆栈为空。在循环中每次弹出栈顶元素，将结果保存在数组中然后再将弹出节点的右子树和左子树一次入栈。首先，例如树

```
   1
  / \
 2   3
/ \ / \
4 5 6 7
```

1. 入栈，执行while循环.
2. 弹出1，将3，2入栈。此时res=\[1\], stack=\[3,2\]
3. 弹出2，将5，4入栈。此时res=\[1, 2\], stack=\[3,5,4\]
4. 弹出4。res=\[1,2,4\], stack=\[3,5\]
5. 弹出5。res=\[1,2,4,5\]. stack=\[3\]
6. 弹出3，将7，6入栈。res=\[1,2,4,5,3\], stack=\[7,6\]
7. 弹出6。res=\[1,2,4,5,3,6\], stack=\[7\]
8. 弹出7。res=\[1,2,4,5,3,6,7\], stack=\[\]
9. 栈为空，循环结束，返回res。

## C++算法

### 递归

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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        helper(root, res);
        return res;
    }
private:
    void helper(TreeNode* root, vector<int>& res){
        if (!root) return;
        res.push_back(root->val);
        if (root->left) helper(root->left, res);
        if (root->right) helper(root->right, res);
    }
};
```

### 迭代

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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        if(!root) return res;
        stack<TreeNode*> stk;
        stk.push(root);
        while(!stk.empty()){
            TreeNode* temp = stk.top();
            stk.pop();
            res.push_back(temp->val);
            if (temp -> right) stk.push(temp->right);
            if (temp -> left) stk.push(temp->left);
        }
        return res;
    }
};
```



