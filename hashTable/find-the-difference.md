## 题目
Given two strings s and t which consist of only lowercase letters.

String t is generated by random shuffling string s and then add one more letter at a random position.

Find the letter that was added in t.

Example:

Input:
s = "abcd"
t = "abcde"

Output:
e

Explanation:
'e' is the letter that was added.

## 题目分析
从t中找出一个跟s不同的字母

## 思路分析
我并没有使用hashtable的思想，而是使用了排序的方法，然后再进行遍历比较，一旦遇到不相同的，则返回t中该字符，否则返回t的最后一个字符

## 代码实现(116ms)
``` javascript
var findTheDifference = function(s, t) {
    s = s.split('').sort().join('');
    t = t.split('').sort().join('');

    for(var i = 0;i<t.length;i++) {
        if(s.charAt(i)!==t.charAt(i)){
            return t.charAt(i);
        }
    }
    return t.charAt(t.length-1);
};
```

然而此方法仅击败了66.4%的js程序，故现奉上比较优秀的js程序(82ms)

``` javascript
var findTheDifference = function(s, t) {
    var n = t.length,c = t.charCodeAt(n - 1);
	for (var i = 0; i < n - 1; i++) {
		c ^= s.charCodeAt(i);
		c ^= t.charCodeAt(i);
	}
	return String.fromCharCode(c);
};
```
