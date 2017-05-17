## 题目
Description:

Count the number of prime numbers less than a non-negative number, n.

## 思路分析
在做这个程序之前须知道，1不是素数，2是素数。
我的解法用了两重循环，其时间复杂度是n^2，然后内层循环是由2到sqrt(i)，若在这区间都没有被整除的数，则其被认为是素数。

## 代码实现
``` javascript
var countPrimes = function(n) {
    var count = 0;
    for(var i = 2;i < n;i++) {
        var flag = false;
        for(var j = 2;j<=Math.floor(Math.sqrt(i));j++) {
            if(i%j===0){
                flag = true;
                break;
            }
        }
        if(!flag){
            count++;
        }
    }
    return count;
};
```
然而我发现这个js程序的耗时极大，需要1136ms，故现在奉上一份耗时只需176ms的js程序，其跟我的只要区别在于，
``` javascript
var countPrimes = function(n) {
    var flag = new Array(n);

    flag[0] = false;
    flag[1] = false;

    var sqr = Math.sqrt(n);
    for(let i = 2; i <= sqr; i++) {//这里循环的次数比起我的循环次数来说要少得多
        if (flag[i] === undefined) {
            var j = i * i;
            //满足j<n的j都不是素数。
            while (j < n) {
                flag[j] = false;
                j += i;
            }
        }
    }

    var count = 0;
    for (let i = 0; i < n; i++) {
      //只要之前没有被设为false的均是素数。
        if (flag[i] === undefined) {
            count++;
        }
    }

    return count;
};
```
