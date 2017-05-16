## 题目
Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

Example 1:
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output:
"apple"
Example 2:
Input:
s = "abpcplea", d = ["a","b","c"]

Output:
"a"

## 思路分析
首先先将d数组排序（以长度排序为主，以ASCII码排序为辅），然后再遍历d数组，第一个匹配的则为结果，（注意：以ASCII顺序排序的方法是`localeCompare`）

## 代码实现
``` javascript
var findLongestWord = function(s, d) {
    //first sorted by str's length second sorted by lexicographical!!!
    d = d.sort(function(a,b){
        if(a.length!==b.length){
            return b.length-a.length;
        }
        //to compare by lexicographical
        return a.localeCompare(b);
    });
    console.log(d);

    //to judge whether the item is the subsequence of the given string or not
    for(var k = 0;k<d.length;k++){
       var item = d[k];
       var i=0,j=0;
       if(item.length>s.length){
           continue;
       }
       while(j<item.length&&i<s.length) {
           if(s[i]===item[j]){
               i++;
               j++;
           }else{
               i++;
           }
       }
       //first match then return the item
       if(j===item.length){
           return item;
       }
    }
    return '';
};
```
