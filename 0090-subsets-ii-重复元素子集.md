[Question](https://leetcode.com/problems/subsets-ii/)
```
Given an integer array nums that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

Example 1:
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]

Example 2:
Input: nums = [0]
Output: [[],[0]]
 
Input: nums = [5,5,5,5,5]
Output: [[],[5],[5,5],[5,5,5],[5,5,5,5],[5,5,5,5,5]]

Constraints:
1 <= nums.length <= 10
-10 <= nums[i] <= 10
```
### 解题思路
数组nums[0,...n-1]这n个数有选或不选两种情况，递归处理这两种情况
由于数组nums有重复元素，先对数组排序，对于重复元素，如果idx>0 && nums[idx]==nums[idx-1], 如果nums[idx-1]没有选择，当前元素也不能选（否则会在结果中有重复）

### 代码

```cpp
class Solution {
public:
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        
        subsetsWithDup(nums, false, 0);
        
        return result;
    }
private:
    void subsetsWithDup(vector<int>& nums, bool preUsed, int idx){
        if(idx == nums.size() ){
            result.emplace_back(subset);
            return ;
        }
        
        //不选当前元素
        subsetsWithDup(nums, false, idx+1);
        
        // 选当前元素
        // 因为有重复元素，所以需要做判断，
        // 如果idx>0 && nums[idx]==nums[idx-1], 如果nums[idx-1]没有选择，当前元素也不能选
        if(idx > 0 && nums[idx] == nums[idx-1] && preUsed == false){
            return ;
        }
        
        subset.emplace_back(nums[idx]);
        subsetsWithDup(nums, true, idx+1);
        subset.pop_back();
    }
    
    vector<vector<int>> result;
    vector<int> subset;
};
```
