## 题目
Divide two integers without using multiplication, division and mod operator.

If it is overflow, return MAX_INT.

## 分析思路
题目说不能使用乘法，除法和取模的运算方式求运算结果，由此可知，除法本质上就是减法，可使用迭代的方式进行计算，其时间复杂度为O(n)，然而结果超时了。

## 代码实现
- 减法**超时**
``` javascript
var divide = function(dividend, divisor) {
    var count = 0;
    while(dividend>=divisor){
        dividend -= divisor;
        count++;
    }
    return count;
};
```

- 移位Accepted
  ``` javascript

  ```
