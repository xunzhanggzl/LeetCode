## 102. 二叉树的层次遍历

[102. 二叉树的层次遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

### 迭代

原理就是 BFS 一层一层地遍历，借助队列实现

这个题的一个小技巧就是 `let len = queue.length;` 这行代码锁住了当前 `for` 循环的次数

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
 * @return {number[][]}
 */
var levelOrder = function (root) {
  if (!root) return [];
  let res = [];
  let queue = [root];
  while (queue.length) {
    let temp = [];
    let len = queue.length;
    for(let i = 0; i < len; i ++) {
      let node = queue.shift();
      node.left && queue.push(node.left);
      node.right && queue.push(node.right);
      temp.push(node.val);
    }
    res.push(temp);
  }
  return res;
};
```

### 递归

原理是 DFS，根据 res 的长度和 depth 比较，如果 `res.length <= depth`，就创建一个空的数组。

这里的 `root.left && dfs(root.left, depth+1);` 和 `root.right && dfs(root.right, depth+1);` 利用了 `JavaScript` 中 `&&` 运算符的原理。

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
 * @return {number[][]}
 */
var levelOrder = function (root) {
  if (!root) return [];
  let res = [];
  function dfs(root, depth) {
    if (res.length <= depth) {
      res[depth] = [];
    }
    res[depth].push(root.val);
    root.left && dfs(root.left, depth+1);
    root.right && dfs(root.right, depth+1);
  }
  dfs(root, 0)
  return res;
};
```

## 103. 二叉树的锯齿形层次遍历

[103. 二叉树的锯齿形层次遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)

### 迭代

大体思路与上一题类似，只是一个奇偶层的判断来决定是 `push` 还是 `unshift`。

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
 * @return {number[][]}
 */
var zigzagLevelOrder = function (root) {
  if (!root) {
    return [];
  }
  let res = [];
  let queue = [root];
  while (queue.length) {
    let len = queue.length;
    let arr = [];
    for (let i = 0; i < len; i++) {
      let treeNode = queue.shift();
      if (res.length % 2 === 0) {
        arr.push(treeNode.val);
      } else {
        arr.unshift(treeNode.val);
      }
      treeNode.left && queue.push(treeNode.left);
      treeNode.right && queue.push(treeNode.right);
    }
    res.push(arr);
  }
  return res;
};
```

### 递归

大体思路与上一题类似，只是一个奇偶层的判断来决定是 `push` 还是 `unshift`。

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
 * @return {number[][]}
 */
var zigzagLevelOrder = function (root) {
  if (!root) {
    return [];
  }
  let res = [];
  let depth = 0;

  function dfs(root, depth) {
    if (res.length <= depth) {
      res[depth] = [];
    }
    if (depth % 2 === 0) {
      res[depth].push(root.val);
    } else {
      res[depth].unshift(root.val);
    }
    root.left && dfs(root.left, depth + 1) 
    root.right && dfs(root.right, depth + 1)
  }
  dfs(root, depth);
  return res;
};
```

