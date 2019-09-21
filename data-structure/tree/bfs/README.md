## 102. 二叉树的层次遍历

### 题目地址

https://leetcode.com/problems/binary-tree-level-order-traversal/description/

### 题目描述

```
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
```

### 思路

这道题可以借助`队列`实现，然后就是while(queue.length), 每次处理一个节点，都将其子节点（在这里是left和right）放到队列中。

在while循环开始时保存当前队列的长度，以保证每次只遍历一层。

> 如果采用递归方式，则需要将当前节点，当前所在的level以及结果数组传递给递归函数。在递归函数中，取出节点的值，添加到level参数对应结果数组元素中。

### 代码

#### 迭代

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
      let x = queue.shift();
      temp.push(x.val);
      x.left && queue.push(x.left);
      x.right && queue.push(x.right);
    }
    res.push(temp);
  }
  return res;
};
```

#### 递归

根据 result 的长度和 depth 比较，如果 `result.length <= depth`，就创建一个空的数组。

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
  let result = [];

  function recursion(root, depth) {
    if (result.length === depth) {
      result[depth] = [];
    }
    result[depth].push(root.val);
    root.left && recursion(root.left, depth + 1);
    root.right && recursion(root.right, depth + 1);
  }
  recursion(root, 0)
  return result;
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

