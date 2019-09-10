## 26. 删除排序数组中的重复项

[26. 删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

为什么返回数值是整数，但输出的答案是数组呢?请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

`给定 nums = [0,0,1,1,1,2,2,3,3,4],函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。你不需要考虑数组中超出新长度后面的元素。`

根据题目的意思，显然不能另外复制一份数组，必须是在原有数组的基础上进行修改，所以不能用 `new Set` 方法

### 使用splice方法

感觉这个题和第27题有bug...

这里唯一需要注意的就是如果相同，`i` 不应该再加一，应该保持不变。

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function (nums) {
  for(let i = 1; i < nums.length; i ++) {
    if (nums[i-1] === nums[i]) {
      nums.splice(i, 1);
      i --;
    }
  }
};
```



## 27. 移除元素

[27. 移除元素](https://leetcode-cn.com/problems/remove-element/)

给定一个数组 nums 和一个值 val，你需要原地移除所有数值等于 val 的元素，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

这个题和第26题有点像

```javascript
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function (nums, val) {
  for (let i = 0; i < nums.length; i ++) {
    if (nums[i] === val) {
      nums.splice(i, 1);
      i --;
    }
  }
};
```


## 169. 求众数

[169. 求众数](https://leetcode-cn.com/problems/majority-element/)

给定一个大小为 n 的数组，找到其中的众数。众数是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

示例 1:

输入: [3,2,3] 输出: 3

示例 2:

输入: [2,2,1,1,1,2,2] 输出: 2

### map

最简单的方法

```javascript
/**
* @param {number[]} nums
* @return {number}
*/
var majorityElement = function (nums) {
  let obj = {};
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] in obj) {
      obj[nums[i]]++;
    } else {
      obj[nums[i]] = 1;
    }
    if (obj[nums[i]] > nums.length / 2) {
      return nums[i];
    }
  }
};
```

### sort

[sort函数 MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function (nums) {
  nums.sort((a, b) => a - b);
  return nums[parseInt(nums.length / 2)]
};
```
