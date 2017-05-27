## 题目
Given two arrays, write a function to compute their intersection.

Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].

Note:
Each element in the result should appear as many times as it shows in both arrays.
The result can be in any order.

## 解题思路
先将数组排序，然后遍历数组，只要相同就Push进arr,不同就自加

## 代码实现
``` javascript
var intersect = function(nums1, nums2) {
  if(nums1.length<1||nums2.length<1){
      return [];
  }
  nums1 = nums1.sort(function(a,b){
      return a - b;
  });

  nums2 = nums2.sort(function(a,b){
      return a - b;
  });


  var i = 0,j = 0,arr = [];
  while(i<nums1.length||j<nums2.length){
      if(nums1[i]===nums2[j]){
          arr.push(nums1[i]);
          i++;
          j++;
      }else if(nums1[i]<nums2[j]) {
          i++;
          while(nums1[i]===nums1[i-1]){
              i++;
          }
      }else{
          j++;
          while(nums2[j]===nums2[j-1]){
              j++;
          }
      }
      if(i===nums1.length||j===nums2.length){
          break;
      }

  }
  return arr;
};
```
然而本代码只是击败了31.5%的js程序，以下是使用hashtable的js程序，其解题思路如下：
先遍历nums1的元素，并且把它们出现的次数记录下来，然后再使用filter方法来筛选出相交的元素
``` javascript
var intersect = function(nums1, nums2) {
    const hash = {};

    nums2.forEach((num) => {
        if (!hash[num]) {
            hash[num] = 1;
        }
        else {
            ++hash[num];
        }
    });

    return nums1.filter((num) => {
        return (hash[num]) && (--hash[num] >= 0);//每遇见一次num,hash[num]就自减
    });
};
```
## 拓展
- What if the given array is already sorted? How would you optimize your algorithm?
  - 使用two pointer
- What if nums1's size is small compared to nums2's size? Which algorithm is better?
  - 将nums1的数值存入hashmap，然后再向nums2进行filter函数调用
- What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?
  - 由题目可知nums1是可以放入内存的，但是内存又有限，所以不支持将nums1存入hashMap，因此要先将则先将nums1进行排序，然后将nums2从磁盘中分块取出，再进行比较呗，比较方法是将nums2的某些片段也进行排序，然后再得出答案。
