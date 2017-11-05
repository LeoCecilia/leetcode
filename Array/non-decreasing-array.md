## 题目
Given an array with n integers, your task is to check if it could become non-decreasing by modifying at most 1 element.

We define an array is non-decreasing if array[i] <= array[i + 1] holds for every i (1 <= i < n).


eg.1
```
Input: [4,2,3]
Output: True
Explanation: You could modify the first
4
 to
1
 to get a non-decreasing array.
```

## 思路
遍历数组，每当arr[i]>arr[i+1]时，count++,此时要比较arr[i-1]和arr[i+1]的关系，然后再根据情况，让arr[1..i]依然成为一个正常的非递减数组。

## 代码实现
``` javascript
var checkPossibility = function(nums) {
    var count = 0;
    for(var i = 0;i<nums.length-1;i++){
        if(nums[i]>nums[i+1]){            
            count++;     
            if (i > 0 && nums[i + 1] < nums[i - 1])
                nums[i + 1] = nums[i];
            else nums[i] = nums[i + 1];
        }
    }
    return count<=1;

};
```
