## 136. 只出现一次的数字

[136. 只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

输入: [2,2,1] 输出: 1

### map

最简单的方法，使用键值对存储

```javascript
/**
* @param {number[]} nums
* @return {number}
*/
var singleNumber = function (nums) {
  let obj = {};
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] in obj) {
      obj[nums[i]]++;
    } else {
      obj[nums[i]] = 1;
    }
  }
  for (let prop in obj) {
    if (obj[prop] === 1) {
      return prop;
    }
  }
};
```

### 异或 ^

相同的两个数异或为 0。 

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function (nums) {
  let res = 0;
  for (let i = 0; i < nums.length; i++) {
    res ^= nums[i];
  }
  return res;
};
```
