## 题目
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## 解题思路
此题中用了一个hash表，感觉还是占用了一丢丢的内存，但是就这样吧。话回正题，要想得到只出现一次的元素，那么用hash表这个数据结构再合适不过啦，然后再用o(2n)即o(n)的时间复杂度便可完成该题目

## 代码实现
``` javascript
var singleNumber = function(nums) {
    var result = {},min = 0,item;
    for(var i = 0;i<nums.length;i++) {
        result[nums[i]] = result[nums[i]]?++result[nums[i]]:1;
    }

    for(var i in result){
        if(result[i]===1){
            return parseInt(i);
        }
    }
};
```

然后我发现了一个另一个更加简洁的方法
``` javascript
var singleNumber = function(arr) {
    var elem = 0;
    for (var i = 0, len = arr.length; i < len; i++) {
        elem = elem ^ arr[i];
    }
    return elem;
};
```
