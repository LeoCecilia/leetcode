## 题目
Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

Examples:
pattern = "abba", str = "dog cat cat dog" should return true.
pattern = "abba", str = "dog cat cat fish" should return false.
pattern = "aaaa", str = "dog cat cat dog" should return false.
pattern = "abba", str = "dog dog dog dog" should return false.
Notes:
You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

## 思路分析
查看是否是同类型，则此题用hash表倒是很好解决，先将str转换为数组arr，然后定义两个哈希表`hashP`,`hashS`，一个用来记录pattern中所有元素的index，另一个则记录arr的。那么若他们的元素对应的索引不一致则返回false，若一致则继续判断
## 代码实现
``` javascript
var wordPattern = function(pattern, str) {
    var arr = str.split(' ');
    if(pattern.length!==arr.length){
        return false;
    }
    var hashP = {},hashS = {};
    for(var i = 0;i<arr.length;i++) {
        if(hashP[pattern[i]]!==undefined&&hashS[arr[i]]!==undefined){
            if (hashS[arr[i]]!==hashP[pattern[i]]){
                return false;
            }
            hashP[pattern[i]] = i;
            hashS[arr[i]] = i;
        }else if(hashP[pattern[i]]===undefined&&hashS[arr[i]]===undefined){
            hashP[pattern[i]] = i;
            hashS[arr[i]] = i;
        }else{
            return false;
        }


    }
    return true;
};
```
