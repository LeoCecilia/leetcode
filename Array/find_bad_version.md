## 题目
Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

## 分析
使用二分查找，可减少isBadVersion的调用次数。<br>出口条件：start>=end，其左边是good version，右边是Bad version，

## 误区
想要在循环当中，便能返回那个bad version，有很多小误区没有考虑到，比如mid-1<1怎么办。。。拓展性不佳

## 代码实现

``` javascript
/**
 * Definition for isBadVersion()
 *
 * @param {integer} version number
 * @return {boolean} whether the version is bad
 * isBadVersion = function(version) {
 *     ...
 * };
 */

/**
 * @param {function} isBadVersion()
 * @return {function}
 */
var solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    return function(n) {
        var start = 1,end = n;
        while(start<end){
            var mid = start+Math.floor((end-start)/2);            
            if(!isBadVersion(mid)){
                start = mid+1;
            }else {
                end = mid;
            }
        }
        return start;

    };
};
```
