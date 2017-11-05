# 题目
You are given an array of positive and negative integers. If a number n at an index is positive, then move forward n steps. Conversely, if it's negative (-n), move backward n steps. Assume the first element of the array is forward next to the last element, and the last element is backward next to the first element. Determine if there is a loop in this array. A loop starts and ends at a particular index with more than 1 element along the loop. The loop must be "forward" or "backward'.

Example 1: Given the array [2, -1, 1, 2, 2], there is a loop, from index 0 -> 2 -> 3 -> 0.

Example 2: Given the array [-1, 2], there is no loop.

# 中文翻译

# 运行代码
``` javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var circularArrayLoop = function(nums) {
    var count = 0,flag = false;
    for(var i = 0;i<nums.length;){
        count+=1;
        i+=nums[i];
        if(i>nums.length-1){
            i = i-nums.length;
            flag = true;
        }
        if(count>1&&i===0){
            if(flag)
                return true;
            
            return false;
        }                
    }
    return false;
};
```