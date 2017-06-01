## 题目
Given a list of strings, you need to find the longest uncommon subsequence among them. The longest uncommon subsequence is defined as the longest subsequence of one of these strings and this subsequence should not be any subsequence of the other strings.

A subsequence is a sequence that can be derived from one sequence by deleting some characters without changing the order of the remaining elements. Trivially, any string is a subsequence of itself and an empty string is a subsequence of any string.

The input will be a list of strings, and the output needs to be the length of the longest uncommon subsequence. If the longest uncommon subsequence doesn't exist, return -1.

Example 1:
Input: "aba", "cdc", "eae"
Output: 3
Note:

All the given strings' lengths will not exceed 10.
The length of the given list will be in the range of [2, 50].
## 题目分析
首先明晰几个概念：
  - subsequence - a是b的subsequence的意思是，a中的元素可从b中的元素删除0个及以上的元素而获得，此乃子集
因此判断a是否是b的子集，只需要先判断a的长度是否比b的大，然后对b进行遍历，只有a[k] === b[i]时，k才自加，若k === a.length，则确认是子集。
关于时间复杂度的问题，因为涉及到相互比较各元素是否是对方的元素的子集，因此其时间复杂度为n(n^2)

## 代码实现
``` javascript
var findLUSlength = function(strs) {
    if(strs.length == 0) return -1;

    var max = -1;
    //相互查看是不是对方的子集
    for (var i = 0; i < strs.length; i++){

        var isLong = true;
        for (var j = 0; j < strs.length; j++){
            if (i == j || strs[j].length < strs[i].length) continue;

            if (isSubSequence(strs[j], strs[i])) {
                isLong = false;
                break;
            }
        }

        if(isLong){
            max = Math.max(max, strs[i].length);
        }
    }

    return max;

    //查看b是不是a的子集
    function isSubSequence(a,b){
        if(a.length<b.length){
            var tmp = a;
            a = b;
            b = a;
        }
        var j = 0;
        for(var i = 0;i<a.length;i++) {
            if(a.charAt(i)===b.charAt(j)){
                j++;
            }
            if(j === b.length){
                return true;
            }
        }
        return false;
    }
};
```
