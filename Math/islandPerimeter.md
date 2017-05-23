## 题目
You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water. Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells). The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

Example:

[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]

Answer: 16
Explanation: The perimeter is the 16 yellow stripes in the image below:
![img](https://leetcode.com/static/images/problemset/island.png)

## 解题思路
遍历二维数组，没遇到一个为1的，result+=4;若是上边或左边有1的，则减去4即可

## 代码实现
``` javaScript
var islandPerimeter = function(grid) {
    if (grid === null || grid.length === 0 || grid[0].length === 0)
        return 0;

    var result = 0;
    for (var i = 0; i < grid.length; i++) {
        for (var j = 0; j < grid[0].length; j++) {
            if (grid[i][j] === 1) {
                result += 4;
                if (i > 0 && grid[i-1][j] === 1)
                    result -= 2;
                if (j > 0 && grid[i][j-1] === 1)
                    result -= 2;
            }
        }
    }
    return result;
};
```
此解法击败了97.5%的js程序，突然觉得自己很厉害啦，现在线上击败了100%的js程序

``` javaScript
var islandPerimeter = function(grid) {
    var perimeter=0;
    for(var i=0; i<grid.length; i++){
        for(var j=0; j<grid[i].length; j++){
            if(grid[i][j]==1){
                if(i-1<0 || grid[i-1][j]==0){
                    perimeter++;
                }
                if(j-1<0 || grid[i][j-1]==0){
                    perimeter++;
                }
                if(i+1>=grid.length || grid[i+1][j]==0){
                    perimeter++;
                }
                if(j+1>=grid[i].length || grid[i][j+1]==0){
                    perimeter++;
                }
            }
        }
    }
    return perimeter;
};
```
其实道理是差不多的，就是感觉有点冗长。
