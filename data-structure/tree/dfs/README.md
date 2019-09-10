## 94. 二叉树的中序遍历

[94.二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

给定一个二叉树，返回它的中序 遍历。

示例:

输入: [1,null,2,3]

输出: [1,3,2]

### 递归

对于中序遍历，就是 `左根右`，`dfs` 递归还是很简单的。

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
 * @return {number[]}
 */
var inorderTraversal = function (root) {
  let res = [];
  function dfs(root) {
    if (root) {
      dfs(root.left);
      res.push(root.val);
      dfs(root.right);
    }
  }
  dfs(root);
  return res;
};
```

### 迭代

如果 `root` 存在，那么将它放入 `stack` 中，并且继续指向左子树。

如果 `root` 不存在，那么取出栈顶元素，将其值放入 `res`，并将 `root` 指向右子树。

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
 * @return {number[]}
 */
var inorderTraversal = function (root) {
  let res = [];
  let stack = [];

  while (stack.length || root) {
    if (root) {
      stack.push(root);
      root = root.left;
    } else {
      let node = stack.pop();
      res.push(node.val);
      root = node.right;
    }
  }
  return res;
};
```




## 98. 验证二叉搜索树

[98. 验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

1. 节点的左子树只包含小于当前节点的数。
2. 节点的右子树只包含大于当前节点的数。
3. **所有左子树和右子树自身必须也是二叉搜索树**。

### DFS + Max + Min

> https://leetcode.com/problems/validate-binary-search-tree/discuss/158094/Python-or-Min-Max-tm

下面的文章写的很详细了，核心就是要传递一个区间。

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
 * @return {boolean}
 */
var isValidBST = function (root) {
  function dfs(root, lowerBound = -Infinity, upperBound = Infinity) {
    if (!root) {
      return true;
    }
    if (root.val <= lowerBound || root.val >= upperBound) {
      return false;
    }
    return dfs(root.left, lowerBound, root.val) && dfs(root.right, root.val, upperBound)
  }
  return dfs(root);
};
```



## 105. 从前序与中序遍历序列构造二叉树

[105. 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
你可以假设树中没有重复的元素。

例如，给出

前序遍历 preorder = [3,9,20,15,7] 中序遍历 inorder = [9,3,15,20,7]

### DFS

这是参考的评论区的一个解法，感觉十分易懂。这里的判断条件就是 `l > r` 是否成立。

```javascript
/**
* Definition for a binary tree node.
* function TreeNode(val) {
*     this.val = val;
*     this.left = this.right = null;
* }
*/
/**
* @param {number[]} preorder
* @param {number[]} inorder
* @return {TreeNode}
*/
var buildTree = function (preorder, inorder) {
  function dfs(l, r) {
    if (l > r) {
      return null;
    }
    let val = preorder.shift();
    let root = new TreeNode(val);
    let index = inorder.indexOf(val);

    root.left = dfs(l, index - 1);
    root.right = dfs(index + 1, r);

    return root;
  }
  return dfs(0, inorder.length - 1)
}
```




## 144. 二叉树的前序遍历

[144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

### 递归

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
 * @return {number[]}
 */
var preorderTraversal = function (root) {
  if (!root) return [];
  let result = [];
  function dfs(root) {
    result.push(root.val);
    root.left && dfs(root.left);
    root.right && dfs(root.right);
  }
  dfs(root);
  return result;
};
```

### 迭代

> Recursive solution is trivial, could you do it iteratively?

在前序后序和中序遍历中，这个的迭代方法应该是最好写的了。

这里注意要运用栈的原理

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
 * @return {number[]}
 */
var preorderTraversal = function (root) {
  if (!root) return [];
  let result = [];
  let stack = [root];
  while (stack.length) {
    let node = stack.pop();
    result.push(node.val);
    node.right && stack.push(node.right);
    node.left && stack.push(node.left);
  }
  return result;
};
```



## 145. 二叉树的后序遍历

[145. 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

### 递归

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
 * @return {number[]}
 */
var postorderTraversal = function (root) {
  if (!root) return [];
  let result = [];
  function dfs(root) {
    root.left && dfs(root.left);
    root.right && dfs(root.right);
    result.push(root.val);
  }
  dfs(root);
  return result;
};
```
