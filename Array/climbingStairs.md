## 题目
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

## 分析
该题用到了数学归纳法，f(1)=1,f(2)=2,f(3)=3,f(4)=5,f(5)=8,由此可知`f(n)=f(n-1)+f(n-2)`，我的代码(99ms)

## 代码实现
``` javascript
var climbStairs = function(n) {
    if(n===1) {
        return 1;
    }
    var a = 1,
        b = 1,
        sum = 0;
    for(var i = 0;i<n-1;i++) {
        sum = a+b;
        a = sum;
        b = tmp;
    }
    return sum;
};
```
## 更佳的代码
最佳的代码应该是递归实现(78ms)
``` javascript
var W = [0, 1, 2];

var climbStairs = function(n) {
    if (W[n] === undefined){
        W[n] = climbStairs(n - 2) + climbStairs(n - 1);
    }

    return W[n];
};
```
