## 题目
Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

Example 1:

Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
Example 2:

Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
## 思路分析
首先先用哈希表将p中的组成情况记录，然后再通过n-slide的方法来遍历s字符串，以得出结果，然而以下的代码实现超时了，现在post上**超时**的代码
``` javascript
var findAnagrams = function(s, p) {
    var resultP = {};
    for(var i = 0;i<p.length;i++) {
        if(resultP[p[i]]){
           resultP[p[i]]++;
        }else{
            resultP[p[i]] = 1;
        }
    }
    var arr = [],key = Object.keys(resultP);
    for(i = 0;i<=(s.length-p.length);i++) {
        var resultS = {};
        for(var j = i;j<(i+p.length);j++) {
            if(resultS[s[j]]){
                resultS[s[j]]++;
            }else{
                resultS[s[j]] = 1;
            }
        }
        var flag = false;
        for(var k = 0;k<key.length;k++) {
            if(resultP[key[k]]!==resultS[key[k]]) {
                flag = true;
                break;
            }
        }
        if(!flag){
            arr.push(i);
        }
    }
    return arr;
};
```

## 代码实现
现在来说说能accepted的代码，首先是先同时记录p的元素组成，以及记录s的前p.length个的字符元素组成，若元素组成相等，则Push进去0index，然后每当i++时候，就将result[s[i-p.length]]的字符减一，并继续记录i字符，并且循环执行到s.length，这样子的时间复杂度便可减少到o(n)啦
``` javascript
var findAnagrams = function(s, p) {
    var resultP = {},resultS = {},arr = [];
    for(var i = 0;i<p.length;i++) {
        if(resultP[p[i]]){
           resultP[p[i]]++;
        }else{
            resultP[p[i]] = 1;
        }

        if(resultS[s[i]]){
            resultS[s[i]]++;
        }else{
            resultS[s[i]] = 1;
        }
    }
    function isEqual(){
        var keys = Object.keys(resultP);
        for(var j = 0;j<keys.length;j++){
            if(resultP[keys[j]]!==resultS[keys[j]]){
                return false;
            }
            if(!resultS[keys[j]]){
                return false;
            }
        }
        return true;
    }
    if(isEqual()){
        arr.push(0);
    }

    for(i = p.length;i<s.length;i++) {
        if(resultS[s[i]]) {
            resultS[s[i]]++;
        }else{
            resultS[s[i]] = 1;
        }
        if(resultS[s[i-p.length]]===1){
            delete(resultS[s[i-p.length]]);
        }else{
			resultS[s[i-p.length]]--;
        }

        if(isEqual()){
            arr.push((i-p.length)+1);
        }
    }

    return arr;

};
```
然而此方法仅击败了11.4%的js程序，故现Post上另一段js代码，减少了对象比较的过程
``` javascript
function getCode(c){
    var code = Math.pow(2, (c.charCodeAt(0) - 97));//97是a的ASCII码
    return code;
}

var findAnagrams = function(s, p) {
    var result = [];
    if(s.length < p.length || p.length === 0)
        return result;

    var pCode = 0, sCode = 0, i;
    for(i = 0; i < p.length; i++){
        pCode += getCode(p[i]);
        sCode += getCode(s[i]);
    }
    if(pCode === sCode)
        result.push(0);

    for(i = 1; i <= s.length - p.length; i++){
        sCode -= getCode(s[i - 1]);
        sCode += getCode(s[i + p.length - 1]);
        if(pCode === sCode)
            result.push(i);
    }        

    return result;
};
```
