```
给你一个整数数组 nums，数组中的元素 互不相同 。返回该数组所有可能的子集（幂集）。
解集不能包含重复的子集。你可以按任意顺序返回解集。
示例 1：
输入：nums = [1,2,3]
输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
示例 2：
输入：nums = [0]
输出：[[],[0]]

提示：
1 <= nums.length <= 10
-10 <= nums[i] <= 10
nums 中的所有元素 互不相同
![image](https://user-images.githubusercontent.com/49578687/123534172-b8ee2300-d74d-11eb-930d-14ffd5ec5b44.png)

Tag：位运算，数组，回溯
```

## Answer
[Discussion Link](https://leetcode.com/problems/subsets/discuss/27278/C%2B%2B-RecursiveIterativeBit-Manipulation)


+ 方法一：每个数都有选或不选两种情况，用递归枚举nums[0,1,…,n-1]这n个数选或不选的情况。
```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
       subsets(nums, 0); 
       return result;
    }
    
private:
    void subsets(vector<int>& nums, int idx){
        if(idx >= nums.size()){
            result.emplace_back(set);
            return ;
        }
	
        // 不选当前元素
        subsets(nums, idx+1);
           
        // 选择当前元素nums[idx]
        set.emplace_back(nums[idx]);
        subsets(nums, idx+1);
           
        // 还原现场
        set.pop_back();
    }
           
    //将结果变量和中间用到的set定义为类变量可以节省在调用函数的过程中需要更多的栈空间
    vector<vector<int>> result;
    vector<int> set;
};
```
+ 方法二：迭代
```
    以[1,2,3]为例，按照如下过程将每个nums[i]元素放入result:
	1) 开始的时候只有一个空的subset [[]];
	2) 添加nums[0]到[] ===>  [ [], [1] ]
	3) 添加nums[1]到 [ [], [1] ] ===>  [ [], [1] , [2], [1,2] ]
	4) 添加nums[2]到 [ [], [1] , [2], [1,2] ] ===> 
	[ [], [1] , [2], [1,2] , [3], [1, 3], [2,3], [1, 2, 3] ]
```
```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> result{{}};
        for(int i = 0; i < nums.size(); i++){
            // 循环遍历之前的每一个result里面的元素，
            // 将nums[i]插入每一个元素中，
            // 然后将新的vector插入result
            int n = result.size();
            for(int j = 0; j < n; j++){
                result.emplace_back(result[j]);
                result.back().emplace_back(nums[i]);
            }
        }
        return result;
    }
};
```
