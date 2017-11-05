## 题目
Find the largest palindrome made from the product of two n-digit numbers.

Since the result could be very large, you should return the largest palindrome mod 1337.

Example:

Input: 2

Output: 987

Explanation: 99 x 91 = 9009, 9009 % 1337 = 987

Note:

The range of n is [1,8].

## 分析
两位数相乘后，并判断其是否是回文，然后再使用`Math.max`获取其最大值。

## 代码实现
** 未ACCEPTED ** 的代码

``` javascript
var largestPalindrome = function(n) {
    var l,h;
    if(n===1){
        l = '0';
        h = '9';
    }else{
        l = '1';
        h = '9';
        for(var i = 0;i<n-1;i++){
            l += '0';
            h += '9';
        }
    }
    l = parseInt(l);
    h = parseInt(h);
    var max = 0;
    for(var x=l,y=l;x<=h,y<=h;x++,y++){
        var value = x*y;
        if(isPalindrome(value+'')){
            Math.max(max,value);
        }
    }
    return max%1337;
};

function isPalindrome(s){
    var l = -1,h = s.length;
    while(++l<--h){
        if(s.charAt(l)!==s.charAt(h))
            return false;
    }
    return true;
}
```


## 正确的解决方案,看不太懂
``` javascript
class Solution {
public:
    int largestPalindrome(int n) {
        if (n == 1) return 9;
        int upper = pow(10, n) - 1;
        int lower = pow(10, n-1);
        for (int i = upper; i >= lower; i--) {
            long cand = buildPalindrome(i);
            for (long j = upper; j*j >= cand; j--) {
                if (cand % j == 0 && cand / j <= upper) {
                    return cand % 1337;
                }
            }
        }
        return -1;
    }

    long buildPalindrome(int n) {
        string s = to_string(n);
        reverse(s.begin(), s.end());
        return stol(to_string(n) + s);
    }
};
```
