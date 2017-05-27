## 题目
Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

## 思路分析
直接使用hash表进行记录元素出现次数，则hash表已出现过，那么就可以返回true，反之返回false

## 代码实现
``` javascript
var containsDuplicate = function(nums) {

    var result = {};
    for(var i = 0;i<nums.length;i++) {
        if(result[nums[i]]){
            return true;
        }else{
            result[nums[i]] = 1;
        }
    }
    return false;
};
```
