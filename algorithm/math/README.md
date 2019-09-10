## 7. 整数反转

[7. 整数反转](https://leetcode-cn.com/problems/reverse-integer/)

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

示例 1:

`输入: 123 输出: 321`

示例 2:

`输入: -123 输出: -321`

示例 3:

`输入: 120 输出: 21`

注意:

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。

这里的一个注意点就是数值的范围。

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function (x) {
  let result = 0;
  while (x != 0) {
    result = result * 10 + x % 10;
    x = parseInt(x / 10);
  }
  if (result < -Math.pow(2, 31) || result > Math.pow(2, 31) - 1) {
    return 0;
  }
  return result;
};
```


## 9. 回文数

[9. 回文数](https://leetcode-cn.com/problems/palindrome-number/)

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:

`输入: 121。输出: true`

示例 2:

`输入: -121。输出: false。解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。`

示例 3:

`输入: 10。输出: false。解释: 从右向左读, 为 01 。因此它不是一个回文数。`

### 对半

一开始想的是要检查到最后，看看两个数是不是完全一样，但是这样会**溢出**如果数字太大的话。

看讨论区提供的思路只检查一半就可以了。

如果给的数小于0或者像120这种的，直接 `return false`。

像 121 这种的，对半检查过后，看是否 `x === parseInt(val / 10)`，像 1221 这种的，对半检查过后，看是否`x === val`。

```javascript
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function (x) {
  if (x < 0 || (x % 10 === 0 && x !== 0)) {
    return false;
  }
  let val = 0;
  while (x > val) {
    val = val * 10 + x % 10; 
    x = parseInt(x / 10);
  }
  return x === val || x === parseInt(val / 10);
};
```

