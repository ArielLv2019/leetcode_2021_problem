[Question](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
```
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。
```
### 解题思路一
+ 自底向上
    + 递归求解左右子树的最大深度，当前深度为max(左右子树深度)+1,
    + 递归终止：root==nullptr，返回0

### 代码

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root == nullptr){
            return 0;
        }
        return max(maxDepth(root->left),  maxDepth(root->right)) + 1;
    }
};
```
### 解题思路二
+ 自顶向下：

### 代码
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        maxDepth(root, 1);
        return result;
    }

private:

    void maxDepth(TreeNode* root, int depth) {
        if(root == nullptr){
            return;
        }
        result = max(result, depth);
        // 递归计算左右子树的depth
        maxDepth(root->left, depth+1);
        maxDepth(root->right, depth+1);
    }

    int result = 0;
};
```
