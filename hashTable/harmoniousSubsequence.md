## 题目
We define a harmonious array is an array where the difference between its maximum value and its minimum value is exactly 1.

Now, given an integer array, you need to find the length of its longest harmonious subsequence among all its possible subsequences.

Example 1:
Input: [1,3,2,2,5,2,3,7]
Output: 5
Explanation: The longest harmonious subsequence is [3,2,2,2,3].

## 思路分析
遍历数组，然后记录每个元素在数组中出现了几次(确实是sequence)，于是遍历哈希表，然后计算result[i]+result[++i]，并且计算出其最大值

## 代码实现
``` javascript
var findLHS = function(nums) {
    var result = {};
    for(var i = 0;i<nums.length;i++) {
        if(result[nums[i]]){
            result[nums[i]]++;
        }else{
            result[nums[i]] = 1;
        }
    }
    var max = 0;
    for(var i in result) {
        var plus = parseInt(i)+1+'';
    		if(result[plus]){
    			max = Math.max(max,result[i]+result[plus]);
    		}        
    }
    return max;
    
};
```
