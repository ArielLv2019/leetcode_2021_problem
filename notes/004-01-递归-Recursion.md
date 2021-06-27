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
