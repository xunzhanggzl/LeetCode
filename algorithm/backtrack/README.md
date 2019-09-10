## 39.组合总和

[39.组合总和](https://leetcode-cn.com/problems/combination-sum/)

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：所有数字（包括 target）都是正整数。解集不能包含重复的组合。 

```
输入: candidates = [2,3,6,7], target = 7,
所求解集为:
[
  [7],
  [2,2,3]
]
```

### 回溯

这里的 `sum` 函数用来计算一个数组的所有元素之和，`backTracking` 函数为回溯函数，`remain` 代表剩余的数组，`temp.push(remain[i]);` 、`backTracking(temp, remain.slice(i));` 、`temp.pop();` 是这个函数的核心。

```javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function (candidates, target) {
  let res = [];
  function backTracking(temp, remain) {
    for(let i = 0; i < remain.length; i ++) {
      temp.push(remain[i]);
      if (sum(temp) === target) {
        res.push(temp.slice());
      }
      if (sum(temp) < target) {
        backTracking(temp, remain.slice(i));
      }
      temp.pop();
    }
  }
  backTracking([], candidates);
  return res;
};

function sum(arr) {
  let Sum = 0;
  arr.forEach(ele => {
    Sum += ele;
  });
  return Sum;
}
```


## 46.全排列

[46.全排列](https://leetcode-cn.com/problems/permutations/)

给定一个**没有重复**数字的序列，返回其所有可能的全排列。

`输入: [1,2,3] 输出: [ [1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1] ]`

### 回溯

`remain.slice(0,i).concat(remain.slice(i+1))` 是这段代码的核心，`remain` 参数代表剩余的数组。

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function (nums) {
  let res = [];

  function backTracking(temp, remain) {
    if (remain.length === 0) {
      res.push(temp.slice());
    }  
    for(let i = 0; i < remain.length; i ++) {
      temp.push(remain[i]);
      backTracking(temp, remain.slice(0,i).concat(remain.slice(i+1)));
      temp.pop();
    }
  }
  backTracking([], nums); 

  return res;
};
```


## 17.电话号码的字母组合

[17.电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

示例:

`输入："23"。输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]`

### 回溯

JavaScript 中 for of 的用法和回溯思想 

回溯思想的核心就是当它到达相应条件时，倒回到上一步。这里的 `for of` 取代 `for` 循环的好处就是可以不用关心字符串的长度。

`prefix.join("")`、`prefix.push(c);`、`prefix.pop();` 是代码的核心。

```javascript
/**
 * @param {string} digits
 * @return {string[]}
 */
const letters = {
  2: 'abc',
  3: 'def',
  4: 'ghi',
  5: 'jkl',
  6: 'mno',
  7: 'pqrs',
  8: 'tuv',
  9: 'wxyz'
};

var letterCombinations = function (digits) {
  let result = [];
  let prefix = [];
  if (digits.length) {
    backTracking(0);
  }

  function backTracking(index) {
    if (index === digits.length) {
      result.push(prefix.join(""));
      return;
    }
    for(let c of letters[digits[index]]) {
      prefix.push(c);
      backTracking(index+1);
      prefix.pop();
    }
  }
  return result;
};
```


## 77.组合

[77.组合](https://leetcode-cn.com/problems/combinations/)

给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。

示例:

输入: n = 4, k = 2
输出: [[2,4],[3,4],[2,3],[1,2],[1,3],[1,4]]

### 回溯

先用 `arr` 把到 n 的一系列数字形成数组，判断条件就是 `temp.length === k` ，`remain` 代表剩余的数字。

```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function (n, k) {
  let res = [];
  let arr = [];
  for(let i = 0; i < n; i ++) {
    arr.push(i+1);
  }
  function backTracking(temp, remain) {
    if (temp.length === k) {
      res.push(temp.slice());
    }
    for(let i = 0; i < remain.length; i ++) {
      temp.push(remain[i]);
      backTracking(temp, remain.slice(i+1));
      temp.pop();
    }
  }
  backTracking([], arr);
  return res;
};
```

## 78. 子集

[78.子集](https://leetcode-cn.com/problems/subsets/)

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:

输入: nums = [1,2,3]
输出: [[],[1],[1,2],[1,2,3],[1,3],[2],[2,3],[3]]

### 回溯

在函数中直接改变了 temp ，因此 `res.push()` 必须是一个 `浅复制（slice）` 的数组，不然到最后 temp 都为空数组。**这个题目中要注意index的作用**。

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsets = function (nums) {
  let res = [];
  function backTracking(temp, index) {
    res.push(temp.slice());
    for(let i = index; i < nums.length; i ++) {
      temp.push(nums[i]);
      backTracking(temp, i+1);
      temp.pop();
    }
  }
  backTracking([], 0);
  return res;
};
```

在传参中改变了 temp，没有使用浅复制，这里注意 `concat` 的作用。

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsets = function (nums) {
  let res = [];

  function backTracking(temp, index) {
    res.push(temp);
    for (let i = index; i < nums.length; i++) {
      backTracking(temp.concat([nums[i]]), i + 1);
    }
  }
  backTracking([], 0);
  return res;
};
```

