## 题目
Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

For example,
Given "egg", "add", return true.

Given "foo", "bar", return false.

Given "paper", "title", return true.

## 解题思路
该题主要是想要哈希表的映射关系，因为s,t都是同一长度的，所以可以在一个循环内进行映射关系的对比。
在遍历字符串中，使用{}这一数据结构来对比，若是`left[s[i]]===right[t[i]]`的话，证明t[i]字符的上一个位置与s[i]字符的上一个位置相同，则继续比较，若是不同，则`return false;`

## 代码实现
``` javascript
var isIsomorphic = function(s, t) {
    var left = {},
        right = {};
    left[s.charAt(0)] = 0;
    right[t.charAt(0)] = 0;
    for(var i = 1;i<s.length;i++) {
        if (left[s[i]] != right[t[i]])
            return false;
        left[s[i]] = i + 1;
        right[t[i]] = i + 1;
    }
    return true;
};
```
