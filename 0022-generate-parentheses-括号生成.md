[Question](
### 解题思路
+ 分治 + 递归
### 代码

```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        // 划分子问题标准：第一个子问题作为不可分割的整体
        // 子段方法：(a)b
        // (a):k对括号，子问题a是k-1对括号
        // b：n-k对括号
        / 生成的括号分成(a)b, 这样就不会出现重复的
        // (a): k对括号，a是k-1对括号
        // b: n-k对括号
        // "()()()" ==> a: "", b:()()
        // "()(())" ==> a: "", b:(())
        // "(())()" ==> a: (), b:()
        // "(()())" ==> a: ()(), b:""
        // "((()))" ==> a: (()), b:""
        if(n == 0){
            return {""}; //如果此处不返回空串"",在for循环中不会进入vector，结果输出为空
        }
        vector<string> result;
        // 不同k之间，加法原理
        for(int k = 1; k <= n; k++){
            auto result_a = generateParenthesis(k-1);
            auto result_b = generateParenthesis(n-k);

            // 左右两个子问题：乘法原理
            for(auto a : result_a){
                for(auto b : result_b){
                    result.emplace_back("(" + a + ")" + b);
                }
            }
        }

        return result;
    }
};
```
### 解题思路二
+ 分治 + 递归 + hash（避免重复计算）
### 代码
```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        // 划分子问题标准：第一个子问题作为不可分割的整体
        // 子段方法：(a)b
        // (a):k对括号，子问题a是k-1对括号
        // b：n-k对括号
        if(n == 0){
            return {""}; //如果此处不返回空串"",在for循环中不会进入vector，结果输出为空
        }
        // 记忆化，避免计算重复的generateParenthesis（）
        if(cache.find(n) != cache.end()){
            return cache[n];
        }
        vector<string> result;
        // 不同k之间，加法原理
        for(int k = 1; k <= n; k++){
            auto result_a = generateParenthesis(k-1);
            auto result_b = generateParenthesis(n-k);

            // 左右两个子问题：乘法原理
            for(auto a : result_a){
                for(auto b : result_b){
                    result.emplace_back("(" + a + ")" + b);
                }
            }
        }
        
        cache[n] = result;
        return result;
    }
private:
    unordered_map<int, vector<string>> cache; //记忆化：加一个缓存，避免重复计算
};
```
