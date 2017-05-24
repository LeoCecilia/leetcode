## 题目
Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note: The solution set must not contain duplicate triplets.

For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]

## 思路分析
首先要将数组进行排序，然后便开始通过一个循环和循环当中的两个指针来进行运算，看看结果是否等于0，若是小于0，证明负数的权重太大，则start++，然后进行检查是否start ==== start-1，若相等，则start++;反之亦然。

## 代码实现
``` javascript
var threeSum = function(nums) {
    if(nums.length<=2) return [];
    var result = [];
    nums = nums.sort(function(a,b){
        return a - b;
    });

    for(var i =0; i < nums.length;){
        var start = i+1, end = nums.length-1;

        while(start < end){
            if(nums[i]+nums[start]+nums[end] === 0){
                result.push([nums[i],nums[start],nums[end]]);
                start++;
                end--;
                while((start < end) && nums[start] === nums[start-1]) start++;
                while((start < end) && nums[end] === nums[end+1]) end--;

            }else if(nums[i]+nums[start]+nums[end]<0){
                start++;
                while((start < end) && nums[start] === nums[start-1]) start++;
            }else{
                end--;
                while((start < end) && nums[end] === nums[end+1]) end--;
            }
        }

        i++;
        while((i < nums.length) && nums[i] === nums[i-1])
            i++;

    }
    return result;
};
```
