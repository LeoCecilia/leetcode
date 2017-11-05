# 题目
给定一个二叉树，如果该树从根部到叶子节点加起来等于sum的路径，则返回true

# 解决方案
该题使用递归最合适。思路如下：路径的走向永远都只有左节点/右节点两种选择，所以递归时，**可使用`||`**

``` javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} sum
 * @return {boolean}
 */
var hasPathSum = function(root, sum) {
    if (root === null) return false;
    if (root.val === sum && root.left ===  null && root.right === null) return true;
    return hasPathSum(root.left, sum-root.val) || hasPathSum(root.right, sum-root.val);
};
```