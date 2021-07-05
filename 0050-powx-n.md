[Question](https://leetcode.com/problems/powx-n/)
```
Implement pow(x, n), which calculates x raised to the power n (i.e., xn).

 

Example 1
Input: x = 2.00000, n = 10
Output: 1024.00000

Example 2:
Input: x = 2.10000, n = 3
Output: 9.26100

Example 3:
Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
 
Constraints:
-100.0 < x < 100.0
-231 <= n <= 231-1
-104 <= xn <= 104
```
#### 解题思路一
+ 递归实现
+ 当n为负数：pow(x, n) = 1/pow(x, -n)
+ 当n为偶数：pow(x, n) = pow(x, n/2) * pow(x, n/2)
+ 当n为奇数：pow(x, n) = pow(x, n/2) * pow(x, n/2) * x
+ 边界递归：pwo(x, 0) = 1
+ T(n) = O(logn)

#### Note:
+ 注意越界，所以将n定义为long long类型
```cpp
// 递归
class Solution {
public:
    // pow(x, n) = pow(x, n/2) * pow(x, n/2); (n为偶数)
    // pow(x, n) = pow(x, n/2) * pow(x, n/2) * x; (n为奇数)
    double myPow(double x, long long n) {
        if(n < 0) { return 1/ myPow(x, -n); }
        if(n == 0) { return 1; }

        double tmp = myPow(x, n/2);
        return n%2==1? tmp*tmp*x : tmp*tmp;
    }
};
```

```cpp
// 循环
class Solution {
public:
    /*
    以pow(x, 5)为例
    初始化： n=5, result = 1;
    while(n > 0){
        n  |  result   | x
        5  |   x       | x(2)
        2  |   x       | x(4)
        1  |   x * x(4)| x(8)
        0  //终止
    }
    
    */
    double myPow(double x, long long n) {
        if(n < 0) { return 1/ myPow(x, -n); }
        double result = 1.0;

        while(n > 0){
            if(n % 2 == 1){
                result *= x;
            }
            x *= x;
            n /= 2;
        }
        return result;
    }
};
```
