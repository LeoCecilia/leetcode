## 题目
Given an array of strings, group anagrams together.

For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"]

## 思路分析
首先遍历数组，将每个元素中的字符串进行ASCII码的排序，然后录入哈希表当中，之后每遍历一个元素，查看hash表中有没有该元素的组成，若有则Push进那个组中，以此达到分组的效果，然而本js程序超时了
``` javascript
var groupAnagrams = function(strs) {
    var result2 = {},arr = [],str;
    //prime = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103];//26个字母
    for(var i = 0;i<strs.length;i++) {
        str = strs[i].split('').sort().join('');
        if(result2[str]!==undefined){
            t = arr[result2[str]];
        }else{    
            t = [];
            arr.push(t);
            var count = Object.keys(result2).length;
            result2[str] = count;
        }
        t.push(strs[i]);

    }

    return arr;
};
```
## 代码实现
``` javascript
var anagrams = function(strs) {
    var map = {},
        len = strs.length,
        curStr,
        newArr,
        sortedArr,
        sortedStr,
        result = [],
        i;

    for (i = 0; i < len; i++) {
        curStr = strs[i];
        sortedArr = curStr.split('');
        sortedStr = sortedArr.sort().join('');

        if (map.hasOwnProperty(sortedStr)) {
            map[sortedStr].push(curStr);
        } else {
            newArr = [];
            newArr.push(curStr);
            map[sortedStr] = newArr;
        }
    }

    len = map.length;

    for (var key in map) {
        if (map[key].length > 1) {
            result = result.concat(map[key]);
        }
    }

    return result;
};
```
