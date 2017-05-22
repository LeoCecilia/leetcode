## 题目
Given an integer array with even length, where different numbers in this array represent different kinds of candies. Each number means one candy of the corresponding kind. You need to distribute these candies equally in number to brother and sister. Return the maximum number of kinds of candies the sister could gain.

Example 1:
Input: candies = [1,1,2,2,3,3]
Output: 3
Explanation:
There are three different kinds of candies (1, 2 and 3), and two candies for each kind.
Optimal distribution: The sister has candies [1,2,3] and the brother has candies [1,2,3], too.
The sister has three different kinds of candies.
Example 2:
Input: candies = [1,1,2,3]
Output: 2
Explanation: For example, the sister has candies [2,3] and the brother has candies [1,1].
The sister has two different kinds of candies, the brother has only one kind of candies.
Note:

The length of the given array is in range [2, 10,000], and will be even.
The number in given array is in range [-100,000, 100,000].

## 解题思路
本题主要是想要算当平均分数组中的数后，小女孩能获得的最多的种类数是多少；那么我们就需要先算出一个有多少种类，然后当sum没有超过数目的一半的时候便自加，若最终仍是没有超过一半，那也无所谓因为我们计算的只是最多的种类，而不是分类结果

## 代码实现
``` javascript
var distributeCandies = function(candies) {
    var len = candies.length/2,
        result = {},
        sum = 0;
    for(var i = 0;i<candies.length;i++) {
        result[candies[i]] = result[candies[i]]?++result[candies[i]]:1;
    }
    for(var item in result){
        if(sum<len){
            sum++;
        }
    }
    return sum;
};
```
然后这只击败了23.73%的javascript程序，现在post上排列较前的程序

``` javascript
var distributeCandies = function(candies) {
    let set = candies.reduce((res, cur) => {
        res.add(cur);
        return res;
    }, new Set());//add()是set的添加元素的方法。感觉这个也挺赞的
    return Math.min(set.size, candies.length / 2);
};
```
