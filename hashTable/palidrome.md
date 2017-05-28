## 题目
Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

Note:
Assume the length of given string will not exceed 1,010.

Example:

Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.

## 解题思路
算入所有元素的偶数个次数，即如果它出现次数是奇数n，则算成count=(n-1)/2，若是偶数n，则直接算成count=n/2，然后如果该对象是一个空对象的话，直接返回2*count,反之，说明期间有奇数，则加上一个即可**因为组成回文串的字符中只能有一个元素出现奇数次**算成2*count+1

## 代码实现
``` javascript
var longestPalindrome = function(s) {
    if(s.length===0){
        return 0;
    }
    var result = {},count = 0;
    for(var i = 0;i<s.length;i++) {
        if(result[s[i]]) {
            delete result[s[i]];
            count++;
        }else{
            result[s[i]] = 1;
        }
    }
    if(Object.keys(result).length !== 0){//查看对象是不是空对象
        return count*2+1;
    }
    return count*2;    
};
```

还有另一种运行时耗更少的代码，其思路与我的一样，只是实现方式不同
``` javascript
var longestPalindrome = function(s) {
    var len = s.length;
    var res = 0;
    var map = {};
    var odd = 0;
    for(var i = 0; i < len; i++){
        if(!map[s[i]])map[s[i]]=0;
        map[s[i]]++;
    }
    for(var key in map){
        if(map[key] % 2 == 0){
            res += map[key];
        }else{
            odd = 1;
            res += map[key] - 1;
        }
    }
    res += odd;
    return res;
};
```
