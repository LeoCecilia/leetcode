## 题目
The count-and-say sequence is the sequence of integers beginning as follows:
1, 11, 21, 1211, 111221, ...

1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.
Given an integer n, generate the nth sequence.

Note: The sequence of integers will be represented as a string.

## 思路分析
每个n的结果主要依赖n-1个结果，这不是很直接的递归思路嘛，而base是当n===1是return的是1，好了现在就可以开始编码啦

## 代码实现
``` javascript
var countAndSay = function(n) {
    if(n===1)
        return '1';
    var before = countAndSay(n-1),
        str = '',
        count = 1;
	  if(before.length===1){
        return '11';
    }
    for(var i = 1;i<before.length;i++){
        if(before[i]===before[i-1]){
            count++;

        }else{
            str += ''+count+''+before[i-1];
		        count = 1;
        }
        if(i===before.length-1){
            str += ''+count+''+before[i];
        }
    }
    return str;
};
```
