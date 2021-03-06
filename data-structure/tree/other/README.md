## 101. 对称二叉树

[101. 对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 `[1,2,2,3,4,4,3]` 是对称的。

### 递归

递归还是比较简单的，如果 `l、r` 都为空返回 `true`，一个为空一个不为空、或者都存在但两者的 `val` 不相等返回 `false`。

```javascript
/**
  * Definition for a binary tree node.
  * function TreeNode(val) {
  * this.val = val;
  * this.left = this.right = null;
  * }
  */
/**
  * @param {TreeNode} root
  * @return {boolean}
  */
var isSymmetric = function (root) {
  if (!root) {
    return true;
  }
  return dfs(root.left, root.right);
};

function dfs(l, r) {
  if (!l && !r) {
    return true;
  }
  if ((!l && r) || (l && !r) || (l.val !== r.val)) {
    return false;
  }
  return dfs(l.left, r.right) && dfs(l.right, r.left);
}
```

### 迭代

借助队列的思想，一层一层地进行比较，其实就是 BFS

```javascript
var isSymmetric = function (root) {
  if (!root) {
    return true;
  }
  let q1 = [root.left];
  let q2 = [root.right];
  while (q1.length || q2.length) {
    let n1 = q1.shift();
    let n2 = q2.shift();
    if (!n1 && !n2) {
      continue;
    }
    if ((n1 && !n2) || (!n1 && n2) || (n1.val !== n2.val)) {
      return false;
    }
    q1.push(n1.left);
    q1.push(n1.right);
    q2.push(n2.right);
    q2.push(n2.left);
  }
  return true;
};
```

