[Question](https://leetcode.com/problems/binary-tree-inorder-traversal/)
```
Given the root of a binary tree, return the inorder traversal of its nodes' values.

Example 1:
Input: root = [1,null,2,3]
Output: [1,3,2]

Example 2:
Input: root = []
Output: []

Example 3:
Input: root = [1]
Output: [1]
```
```cpp
// 递归
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        seq = new ArrayList<Integer>();
        find(root);
        
        return seq;
    }
    
    private void find(TreeNode root){
        if(root == null){
            return ;
        }
        
        find(root.left);
        seq.add(root.val);
        find(root.right);
    }
    private List<Integer> seq;
}
```
