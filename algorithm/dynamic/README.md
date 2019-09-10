## 53.最大子序和

[53.最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

```
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

### 动态规划

下面这个解法的思想就是从一开始就求出到该位置的最大子序和，然后直接返回其中的最大值。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function (nums) {
  for (let i = 1; i < nums.length; i++) {
    nums[i] = Math.max(nums[i-1] + nums[i], nums[i]);
  }
  console.log(nums); // [-2, 1, -2, 4, 3, 5, 6, 1, 5]
  return Math.max(...nums);
};
maxSubArray([-2,1,-3,4,-1,2,1,-5,4]);
```



## 70. 爬楼梯

[70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

假设你正在爬楼梯。需要 *n* 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**注意：**给定 *n* 是一个正整数。

示例 1：

输入： 2  输出： 2  解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶

示例 2：

输入： 3  输出： 3  解释： 有三种方法可以爬到楼顶。

1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶

### 递归

下面这个是一开始的做法，结果发现时间超限，这个题类似于 **斐波那契数列**，可以查看《剑指offer》的第75页，时间超限的原因是一个运算有时会进行很多次。

```javascript
/**
* @param {number} n
* @return {number}
*/
var climbStairs = function (n) {
    if (n === 1) {
        return 1;
    }
    if (n === 2) {
        return 2 
    }
    return climbStairs(n - 1) + climbStairs(n - 2)
};
```

### 备忘录哈希表

类似 **斐波那契数列** 的解法

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function (n) {
    if (n === 1) {
        return 1;
    }
    let arr = [1,2]
    for(let i = 2; i < n; i ++) {
        arr[i] = arr[i-1] + arr[i-2];
    }
    return arr[n-1];
};
```

### 动态规划

优化：其实不需要数组，运用了一下ES6的 **解构**

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function (n) {
    if (n === 1) {
        return 1;
    }
    let a = 1;
    let b = 2;
    for(let i = 2; i < n; i ++) {
        [a, b] = [b, a+b]
    }
    return b;
};
```