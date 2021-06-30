## 递归
### 递归的三个关键
+ 1）定义需要递归的问题（重叠子问题） ---- 数学归纳法思维
+ 2）确定递归边界
+ 3）保护与还原现场（具体问题具体分析，有的题目不需要，对于参数和局部变量不需要做此操作，  全局变量如class的变量需要）

### 模板
```cpp
void recursion(int level, int param){
  //terminator终止条件
  if(level > MAX_LEVEL){
    // processor result: 处理结果
    return ;
  }
  
  // process login in current level: 处理当前递归层的逻辑
  process(level, param);
  
  // drill down: 继续往下递归调用
  recursion(level+1, new_parar);
  
  // restore the current level status: 恢复当前层的状态
}
  
```

### 实战题目
[78子集](https://github.com/ArielLv2019/leetcode_2021_problem/blob/main/0078-E-subsets-%E5%AD%90%E9%9B%86.md)
[90-子集II](https://github.com/ArielLv2019/leetcode_2021_problem/blob/main/0090-subsets-ii-%E9%87%8D%E5%A4%8D%E5%85%83%E7%B4%A0%E5%AD%90%E9%9B%86.md)
[77组合](https://github.com/ArielLv2019/leetcode_2021_problem/blob/main/0077-combination-%E7%BB%84%E5%90%88.md)
[46-全排列](https://github.com/ArielLv2019/leetcode_2021_problem/blob/main/0046-permutations-%E5%85%A8%E6%8E%92%E5%88%97.md)
[47-全排列II](https://github.com/ArielLv2019/leetcode_2021_problem/blob/main/0047-permutations-ii-%E5%85%A8%E6%8E%92%E5%88%97.md)

## 树
### 介绍
+ 重叠子问题： 翻转or验证左右子树
+ 当前层逻辑：翻转or验证大小关系
+ 递归边界： 叶子节点（无子树，即root==nullptr）

### 实战题目
[26-翻转二叉树](https://github.com/ArielLv2019/leetcode_2021_problem/blob/main/0026-invert-binary-tree-%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91.md)
[98-验证二叉搜索树](https://github.com/ArielLv2019/leetcode_2021_problem/blob/main/0098-validate-binary-search-tree-%E9%AA%8C%E8%AF%81%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.md)
[104-二叉树的最大深度](https://github.com/ArielLv2019/leetcode_2021_problem/blob/main/0104-maximum-depth-of-binary-tree-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.md)
[111-二叉树的最小深度](https://github.com/ArielLv2019/leetcode_2021_problem/blob/main/0111-minimum-depth-of-binary-tree-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%B0%8F%E6%B7%B1%E5%BA%A6.md)
