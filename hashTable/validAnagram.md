## 题目
Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

Note:
You may assume the string contains only lowercase alphabets.

## 思路分析
因为不懂得怎么用hashMap，这里我仍然沿用了排序的方法来完成

## 代码实现
``` javascript
var isAnagram = function(s, t) {
    s = s.split('').sort().join('');
    t = t.split('').sort().join('');

    if(s.length!==t.length){
        return false;
    }

    for(var i = 0;i<s.length;i++) {
        if(s.charAt(i)!==t.charAt(i)) {
            return false;
        }
    }

    return true;
};
```
然而此方法仅击败了26.5%的js程序，故现在线上运用了hashTable的js程序

``` javascript
var isAnagram = function(s, t) {
  //我先前就差了考虑这一步，如果两者都不想等，谈何重组
  if (s.length !== t.length)
    return false;

  var hashMap = {};
  for (var i = 0; i < s.length; i++) {
    //若存在则加一，否则设为1
    hashMap[s[i]] = hashMap[s[i]] ? hashMap[s[i]] + 1 : 1;
  }

  for (i = 0; i < t.length; i++) {
    if (hashMap[t[i]]) {
      hashMap[t[i]]--;
    } else {
      //若没有则返回true
      return false;
    }
  }

  return true;
};
```
