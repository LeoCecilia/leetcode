## 题目
Given a List of words, return the words that can be typed using letters of alphabet on only one row's of American keyboard like the image below.

## 思路分析
只需要把字母的行数收录到hash表中，再将第二个数组中的字符串的所有元素转换成小写，然后再对比他们是不是同一行的就行啦
## 代码实现
```javascript
var findWords = function(words) {
    var str = ["qwertyuiop","asdfghjkl","zxcvbnm"],
        result = [];
    for(var i = 0;i<str.length;i++) {
        for(var j = 0;j<str[i].length;j++) {
            result[str[i][j]] = i;
        }
    }
    var arr = [];
    for(i = 0;i<words.length;i++) {
        var flag = false;
        for(var k = 0;k<words[i].length-1;k++) {
            if(result[words[i][k].toLowerCase()]!==result[words[i][k+1].toLowerCase()]){
                flag = true;
                break;
            }
        }
        if(!flag){
            arr.push(words[i]);
        }

    }
    return arr;
};
```
