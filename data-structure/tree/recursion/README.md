## 104. 二叉树的最大深度

[104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

### BFS

下面这种方法在写的时候遇到过一个大坑：`while([])`  会死循环导致时间超限，因为 `Boolean([]) === true`，发生了隐式的强制类型转换。

还是用 `len` 锁住 `for` 循环的次数。

> https://dorey.github.io/JavaScript-Equality-Table/

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function (root) {
  if (!root) return 0;
  let depth = 0;
  let queue = [root];
  while (queue.length) {
    let len = queue.length;
    for(let i = 0; i < len; i ++) {
      let node = queue.shift();
      node.left && queue.push(node.left);
      node.right && queue.push(node.right);
    }
    depth ++;
  }
  return depth;
};
```

### DFS

```javascript
var maxDepth = function (root) {
    if (!root) return 0;
    return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
};
```