## 题目
Given a collection of distinct numbers, return all possible permutations.

For example,
[1,2,3] have the following permutations:
```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
## 解决思路
其使用了全排列的算法，[2,1,3],[3,2,1]是由[1,2,3]中的第一个元素和后面的元素交换得来的，而[2,3,1]则是由[2,1,3]的第二个和第三个元素交换得来的，同理[1,3,2]亦是由第二个元素和第三个元素交换得来的，由此可知，全排列算法的精髓是**从第一个元素开始，分别与后面的元素交换而获得的元素**


## 代码实现
``` javascript
var permute = function(nums) {
    //从第1个数开始，分别与后面的数进行交换的过程
    var permutation = [],
        arr = nums;
    function swap(a,b) {
        var tmp = arr[a];
        arr[a] = arr[b];
        arr[b] = tmp;
    }
    function combine(){
      var tmp = [];
      for(var i = 0;i<arr.length;i++) {
        tmp.push(arr[i]);
      }
      return tmp;
    }
    function generate(start) {
        if(start === arr.length-1) {
            permutation.push(combine());
            //这里不能直接使用permutaion.push(arr);，这样会使得permutation中所有的元素都一样的，其实并不知道这是为什么
        }else{
            for(var i = start;i<arr.length;i++) {
                swap(start,i);
                generate(start+1);
                swap(start,i);
            }
        }
    }
    generate(0);
    return permutation;
};
```
这是已经Accepted的想法，但不是最优的代码，一下Post上击败100%的js代码

---

``` javascript
var permute = function(nums) {
    var results = [];
    recurse(nums, 0, results);
    return results;
};



var recurse = function(nums, startIdx, results) {
    if (startIdx==nums.length-1)
        results.push(nums.slice(0));
    else {
        for (var i = startIdx; i < nums.length; i++) {
            swap(nums, startIdx, i);
            recurse(nums, startIdx+1, results);
            swap(nums, startIdx, i);
        }
    }
};

var swap = function(nums, i, j) {
    var tmp = nums[i];
    nums[i] = nums[j];
    nums[j] = tmp;
};
```
## 总结
js的原生方法的效率远比用循环高许多，要时刻记住去使用原生的方法。
