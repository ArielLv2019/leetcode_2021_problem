[Question](https://leetcode.com/problems/validate-binary-search-tree/)
```
给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
节点的右子树只包含大于当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。
示例 1:

输入:
    2
   / \
  1   3
输出: true
示例 2:

输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。

```
### 解题思路
    /*
        节点的左子树只包含小于当前节点的数。-> 左子树的最大节点比根节点小
        节点的右子树只包含大于当前节点的数。-> 右子树的最小节点比根节点大
        所有左子树和右子树自身必须也是二叉搜索树。
    */
    /*
        要完成如下三件事情：
        1） 验证根节点比左子树的最大节点大，
        2） 验证根节点比右子树大最小节点小
        3） 递归验证左右子树
    */

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

    bool isValidBST(TreeNode* root) {
        TreeNode* minNode = nullptr;
        TreeNode* maxNode = nullptr;
        return isValidBST(root, minNode, maxNode);
    }

private:
    bool isValidBST(TreeNode* root, TreeNode* minNode, TreeNode* maxNode) {
        if(root == nullptr){
            return true;
        }
        // root的值要满足: minVal < root < maxVal
        if(minNode != nullptr && root->val <= minNode->val){
            return false;
        }
        if(maxNode != nullptr && root->val >= maxNode->val){
            return false;
        }
        // 左子树的节点都要小于根节点  && 右子树都节点都要大于根节点
        return isValidBST(root->left, minNode, root) && isValidBST(root->right, root, maxNode);
    }
};
```
