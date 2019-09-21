## 94. 二叉树的中序遍历

### 题目地址

https://leetcode-cn.com/problems/binary-tree-inorder-traversal/

### 题目描述

```
Given a binary tree, return the inorder traversal of its nodes' values.

Example:

Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
Follow up: Recursive solution is trivial, could you do it iteratively?
```

### 思路

递归的方式相对简单，非递归的方式借助栈这种数据结构实现起来会相对轻松。

如果采用非递归，可以用栈(Stack)的思路来处理问题。

中序遍历的顺序为左-根-右，具体算法为：

- 从根节点开始，先将根节点压入栈
- 然后再将其所有左子结点压入栈，取出栈顶节点，保存节点值
- 再将当前指针移到其右子节点上，若存在右子节点，则在下次循环时又可将其所有左子结点压入栈中， 重复上步骤

### 代码

#### 递归

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
  if(!root) return [];
  let result = [];
  function recursion(root) {
    root.left && recursion(root.left);
    result.push(root.val);
    root.right && recursion(root.right);
  }
  recursion(root);
  return result;
};
```

#### 迭代

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
  let result = [];
  let stack = [];

  while (stack.length || root) {
    if (root) {
      stack.push(root);
      root = root.left;
    } else {
      let x = stack.pop();
      result.push(x.val);
      root = x.right;
    }
  }
  return result;
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

### 题目地址

https://leetcode-cn.com/problems/binary-tree-preorder-traversal/

### 题目描述

```
Given a binary tree, return the preorder traversal of its nodes' values.

Example:

Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]
Follow up: Recursive solution is trivial, could you do it iteratively?
```

### 思路

前序遍历是`根左右`的顺序，注意是`根`开始，那么就很简单。直接先将根节点入栈，然后 看有没有右节点，有则入栈，再看有没有左节点，有则入栈。 然后出栈一个元素，重复即可。

### 代码

#### 递归

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
  function recursion(root) {
    result.push(root.val);
    root.left && recursion(root.left);
    root.right && recursion(root.right);
  }
  recursion(root);
  return result;
};
```

#### 迭代

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
    let x = stack.pop();
    result.push(x.val);
    x.right && stack.push(x.right);
    x.left && stack.push(x.left);
  }
  return result;
};
```



## 145. 二叉树的后序遍历

### 题目地址

https://leetcode.com/problems/binary-tree-postorder-traversal/description/

### 题目描述

```
Given a binary tree, return the postorder traversal of its nodes' values.

For example:
Given binary tree {1,#,2,3},

   1
    \
     2
    /
   3
 

return [3,2,1].

Note: Recursive solution is trivial, could you do it iteratively?
```

### 思路

相比于前序遍历，后续遍历思维上难度要大些，前序遍历是通过一个stack，首先压入父亲结点，然后弹出父亲结点，并输出它的value，之后压人其右儿子，左儿子即可。

然而后序遍历结点的访问顺序是：左儿子 -> 右儿子 -> 自己。那么一个结点需要两种情况下才能够输出： 第一，它已经是叶子结点； 第二，它不是叶子结点，但是它的儿子已经输出过。

那么基于此我们只需要记录一下当前输出的结点即可。对于一个新的结点，如果它不是叶子结点，儿子也没有访问，那么就需要将它的右儿子，左儿子压入。 如果它满足输出条件，则输出它，并记录下当前输出结点。输出在stack为空时结束。

### 代码

#### 递归

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

#### 迭代

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
var postorderTraversal = function(root) {
  if (!root) return [];
  let stack = [root];
  let result = [];

  while (stack.length) {
    let x = stack.pop();
    result.unshift(x.val);
    x.left && stack.push(x.left);
    x.right && stack.push(x.right);
  }

  return result;
}
```

