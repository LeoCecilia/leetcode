## 题目
Given n points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points (i, j, k) such that the distance between i and j equals the distance between i and k (the order of the tuple matters).

Find the number of boomerangs. You may assume that n will be at most 500 and coordinates of points are all in the range [-10000, 10000] (inclusive).

## 思路分析
本题给予我们定义了一个新的数据结构，就是a,b,c三点中，如果b到a的距离与c到a的距离相等，则成为boomerang，然后题目让找出一个数组当中有多少个符合boomerang的数据结构;分析：如果abc是boomerang的话，那么就有两种组合方式：abc，acb，如果有3个点到a点的距离都相等的话，则有6种方式；其实就是从n个中选择2个来跟a来做排列组合嘛，所以结果就是n(n-1)咯，那么具体做法就是，遍历points,让每一个点都做一次a，然后计算其他点与a间的距离，用哈希表来存储，以距离为键，以个数为键值。而只有个数超过2(有距离相等的点)，就进行累加即可
## 代码实现
``` javascript
var numberOfBoomerangs = function(points) {
    var sum = 0;
    for(var i = 0;i<points.length;i++) {
        var result = {};
        for(var j = 0;j<points.length;j++) {
            if(i!==j) {
				var a = points[j][0] - points[i][0];
                var b = points[j][1] - points[i][1];
                if(result[a*a+b*b]!==undefined){
                    result[a*a+b*b]++;
                }else{
                    result[a*a+b*b] = 1;
                }
            }            

        }
        for(var k in result){
            if(result[k]>=2){
                sum += result[k]*(result[k]-1);
            }
        }                
    }

    return sum;
};
```
