## 题目
Given two binary strings, return their sum (also a binary string).

For example,
a = "11"
b = "1"
Return "100".

## 思路分析
要注意进位

## 代码实现
``` javascript
var addBinary = function(a, b) {
    var i = a.length - 1,
        j = b.length - 1;
    var cf = 0,
        sum = '',
        tmp;
    while(i>=0||j>=0){
        posa = parseInt(a[i]) || 0;
        posb = parseInt(b[j]) || 0;
        tmp = posa+posb+cf;
        cf = Math.floor(tmp/2);
        sum = (tmp%2)+''+sum;//这里挺重要的，直接逆序，不用在最后，是用sum.split('').reverse().join('')
        i--;
        j--;
    }
    if(cf){
        sum = ''+cf+sum;
    }
    return sum;
};
```
