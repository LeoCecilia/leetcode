## 题目
Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.

## 思路分析
探测是否重复，若重复，且其坐标值差值<=k则返回true,此题主要使用hash表即可解决

## 代码实现
``` javascript
var containsNearbyDuplicate = function(nums, k) {
    var result = {};
    for(var i = 0;i<nums.length;i++) {
        if(result[nums[i]]!==undefined&&i-result[nums[i]]<=k){
            return true;
        }
        result[nums[i]] = i;
    }
    return false;
};
```
