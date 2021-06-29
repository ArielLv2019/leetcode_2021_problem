[Question](https://leetcode.com/problems/permutations/)
```
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

Example 1:
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Example 2:
Input: nums = [0,1]
Output: [[0,1],[1,0]]

Example 3:
Input: nums = [1]
Output: [[1]]
```
### 解题思路一
+ 依次考虑[0, n-1]位置放哪个数，
+ “从还没用过的数”中选一个放在当前位置

### 代码

```cpp
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        used = vector<bool>(nums.size(), false);
        permute(nums, 0);
        return result;
    }
    
private:
    // 依次考虑[0, n-1]位置放哪个数，
    // “从还没用过的数”中选一个放在当前位置
    void permute(vector<int>& nums, int idx){
        if(idx == nums.size()){
            result.emplace_back(per); // 其他语言需要make a copy; 以python为例： self.ans.append(self.per[:])
            return;
        }
        // 从还没有用过的数里面选一个，考虑所有没有用过的数
        for(int i = 0; i < nums.size(); i++){
            if(!used[i]){ //下标为i的数还没有用过
                per.emplace_back(nums[i]);
                used[i] = true;
                
                // 去找下一个位置填什么
                permute(nums, idx+1);
                
                //还原现场
                used[i] = false;
                per.pop_back();
            }
        }
        
        return ;
    }
    
    vector<vector<int>> result;
    vector<int> per;
    vector<bool> used;
};
```
```cpp
// cpp: recursive(递归）
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> result;
        permute(nums, result, 0);
        return result;
    }
private:
    void permute(vector<int>& nums, vector<vector<int>>& result, int begin){
        if(begin >= nums.size()){
            result.emplace_back(nums);
            return;
        }
        
        for(int i = begin; i < nums.size(); i++){
            swap(nums[i], nums[begin]);
            permute(nums, result, begin+1);
            swap(nums[i], nums[begin]); //reset
        }
        
        return ;
    }
};
```
