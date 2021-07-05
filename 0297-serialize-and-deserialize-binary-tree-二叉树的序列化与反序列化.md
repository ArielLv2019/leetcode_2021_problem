[Question](https://leetcode.com/problems/serialize-and-deserialize-binary-tree)
```
序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

提示: 输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 LeetCode 序列化二叉树的格式。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。 

示例 1：
输入：root = [1,2,3,null,null,4,5]
输出：[1,2,3,null,null,4,5]
示例 2：
输入：root = []
输出：[]

示例 3：
输入：root = [1]
输出：[1]

示例 4：
输入：root = [1,2]
输出：[1,2]
```
### 解题思路一
+ 用先序访问实现

### 代码

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
class Codec {
public:

    // Encodes a tree to a single string.
    // 1，2，null, 3, 4, null, null, 5, null, null
    string serialize(TreeNode* root) {
        preorder(root);

        // vector to string
        // stringstream result;
        // copy(seq.begin(), seq.end(), ostream_iterator<string>(result, "\n"));
        // return result.str();
        string result;
        for(auto s : seq){
            result += s + " ";
        }

        result.pop_back(); // 移走最后一个空格
        return result;
    }

    // Decodes your encoded data to tree.
    // 用递归： 依次复原根->左->右
    // [1，2，null, 3, 4, null, null, 5, null, null]
    // idx= 0, 先复原data[0],
    TreeNode* deserialize(string data) {
        seq = splitString(data, " ");
        // for(auto s : seq){
        //     cout<< s << ",";
        // }
        curIdx = 0;       
        return calc();
        return nullptr;
    }

private:
    // 先序：[1，2，null, 3, 4, null, null, 5, null, null]
    void preorder(TreeNode* root){
        if(root == nullptr){
            seq.emplace_back("null");
            return;
        }
        seq.emplace_back(to_string(root->val));
        preorder(root->left);
        preorder(root->right);
    }
    
    TreeNode* calc(){
        if(seq[curIdx] == "null"){ // 对于null的值返回空指针
            curIdx++;  //当前curIdx所指的节点已经处理完，往后移动下标
            return nullptr;          
        }

        TreeNode* root = new TreeNode(stoul(seq[curIdx]));
        curIdx++; //当前curIdx所指的节点已经处理完，往后移动下标
        root->left = calc();
        root->right = calc();
        return root;
    }

    vector<string> splitString(string& str, string pattern){
        vector<string> result;
        str += pattern; // 扩展字符串以方便操作
        
        for(int i = 0; i < str.size(); ){
            int pos = str.find(pattern, i);
            result.push_back(str.substr(i, pos-i)); // substr(pos, count)       
            i = pos + pattern.size();
        }
        return result;
    }
    // 先序：[1，2，null, 3, 4, null, null, 5, null, null]
    vector<string> seq;
    int curIdx;
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```
### 解题思路二
+ 也可以访问树，得到树的前序和中序的遍历结果，
+ 从前序和中序的遍历结构构造树，参考题105
