## 题目
Given a string, find the length of the longest substring without repeating characters.<br>
即找出**没有重复**字符的**连续**字符串的**最长**长度

Examples:

Given `"abcabcbb"`, the answer is `"abc"`, which the length is 3.

Given `"bbbbb"`, the answer is `"b"`, with the length of 1.

Given `"pwwkew"`, the answer is `"wke"`, with the length of 3. Note that the answer must be a substring, `"pwke"` is a subsequence and not a substring.

## 解决思路
用start来存储没有重复字符的起点位置，而每当一段连续的字符遇到重复(前提是result[s[i]]的值要比start的大，这说明那是新的没有重复字符的连续字符串)的字符时，便通过`max = Math.max(max,i-start)`的方法来判断其长度是否比先前的长，将其赋值给max，这里使用对象来判断是否遇到重复起点(若`result[s[i]])`大于start，则肯定是遇到重复字符，然后再向`result[s[i]]`赋当前的i值

## 代码实现
``` javascript
var lengthOfLongestSubstring = function(s) {
    var max = 0,
        start = -1,
        result = {};
    for(var i = 0;i<s.length;i++) {
        if(result[s[i]]>start)
            start = result[s[i]];
        result[s[i]]=i;
        max = Math.max(max,i-start);
    }
    return max;
};
```
