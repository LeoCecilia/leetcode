# 题目
Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

For example:

* Given numerator = 1, denominator = 2, return "0.5".
* Given numerator = 2, denominator = 1, return "2".
* Given numerator = 2, denominator = 3, return "0.(6)".

# 思路
此题关键在于何时会出现循环小数

> 误区：认为当有相同商的时候，便会出现循环小数。。
> 反驳：66/2=33

所以当我们笔算除法的时候，会发现当余数相同且**不为0**的时候，便会出现循环小数

注意的坑

* 求余结果的正负号，取决于被除数
* 所以应先将两个数值变成正数
* 使用hash表记录当前余数所在的位置
* 总之要模拟笔算除法的过程

``` javascript
/**
 * @param {number} numerator
 * @param {number} denominator
 * @return {string}
 */
var fractionToDecimal = function(numerator, denominator) {
    if(numerator===0)
        return '0';
    var ret = [];
    if(numerator<0 ^ denominator<0)
        ret.push('-');
    numerator = Math.abs(numerator);
    denominator = Math.abs(denominator);
    ret.push(Math.floor(numerator/denominator));
    
    if(numerator%denominator===0)
        return ret.join('');
    ret.push('.');
    var map = {};
    for(var r = numerator % denominator; r; r%=denominator){
        if(map.hasOwnProperty(r)){
            ret.splice(map[r],0,'(');
            ret.push(')');
            break;
        }
        map[r] = ret.length;
        //尝试自己笔算
        r*=10;
        ret.push(Math.floor(r/denominator));
    }
    return ret.join('');
};
```