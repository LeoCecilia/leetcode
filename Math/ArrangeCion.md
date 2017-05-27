## 题目
You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

Example 1:

n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
Example 2:

n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.

## 思路分析
由图像可知，只要1+...+n<=8即可由此可列出公式n(n+1)/2<=8，然后根据解题公式即可算出n

## 代码实现
``` javascript
var arrangeCoins = function(n) {
  return Math.floor((-1+Math.sqrt(1+8*n))/2);
};
```

然而这击败了87.5%的js程序，现在要呈现另一个击败100%的js程序，其使用了按位运算的思路，来实现去除小数的功能，但其与`Math.floor`的不同之处在于`~~`只删除小数，而不会改变整数本身的数值，不进行舍入操作。

``` javascript
var arrangeCoins = function(n) {
  return ~~((-1+Math.sqrt(1+8*n))/2);
};
```
