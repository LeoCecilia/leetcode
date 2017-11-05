## 题目
Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome.

## 分析
先定义一个判断是否是回文的function，然后再在validPaLindrome使用递归，从两端遍历字符串，当第一次发现不等时，“删掉”l/h，判断剩下的字符串是否为回文

## 代码实现
``` javascript
var validPalindrome = function(s) {
    var l = -1,h = s.length;
    while(++l<--h){
        if(s.charAt(l)!==s.charAt(h)){
            //删掉l或者删除h
            return isPalindrome(s,l,h+1) || isPalindrome(s,l-1,h);
        }
    }
    return true;
};

function isPalindrome(s,l,h){
    while(++l<--h){
        if(s.charAt(l)!==s.charAt(h))
            return false;
    }
    return true;
}
```
