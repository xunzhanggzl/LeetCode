## 1. 两数之和

[1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

`给定 nums = [2, 7, 11, 15], target = 9 因为 nums[0] + nums[1] = 2 + 7 = 9。 所以返回 [0, 1]`

### 对象

使用普通的 `{}` 来存储键值对。

```javascript
/**
* @param {number[]} nums
* @param {number} target
* @return {number[]}
*/
var twoSum = function (nums, target) {
  let obj = {};
  for(let i = 0; i < nums.length; i ++) {
    let key = nums[i];
    if (key in obj) {
      return [obj[key], i];          
    }
    obj[target-key] = i;
  }
};
```

### Map

用 ES6 新增语法 Map 存储键值对。这个解法中使用了 Map 的三个方法。

1. `Map.prototype.set(key, value)`
2. `Map.prototype.has(key)`
3. `Map.prototype.get(key)`

> **Map** 对象保存键值对。任何值(对象或者[原始值](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)) 都可以作为一个键或一个值。

```javascript
/**
* @param {number[]} nums
* @param {number} target
* @return {number[]}
*/
var twoSum = function (nums, target) {
  let myMap = new Map();
  for (let i = 0; i < nums.length; i++) {
    let key = nums[i];
    if (myMap.has(key)) {
      return [myMap.get(key), i];
    }
    myMap.set(target - nums[i], i);
  }
};
```


## 217. 存在重复元素

[217. 存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

示例 1:

输入: [1,2,3,1] 输出: true

示例 2:

输入: [1,2,3,4] 输出: false

### 先排序

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function (nums) {
  let len = nums.length;
  nums.sort((a, b) => a - b);
  for (let i = 1; i < len; i++) {
    if (nums[i - 1] === nums[i]) {
      return true;
    }
  }
  return false;
};
```

### 使用map

下面这样使用 `{}` 会检测不到 0 的重复，如 `[0,4,5,0,3,6]` 

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function (nums) {
  let len = nums.length;
  let obj = {};
  for (let i = 0; i < len; i++) {
    if (!obj[nums[i]]) {
      obj[nums[i]] = nums[i];
      console.log(obj)
    } else {
      return true;
    }
  }
  return false;
};

// 可以看到检测不到 0 的重复
{ '0': 0 }
{ '0': 0, '4': 4 }
{ '0': 0, '4': 4, '5': 5 }
{ '0': 0, '4': 4, '5': 5 }
{ '0': 0, '3': 3, '4': 4, '5': 5 }
{ '0': 0, '3': 3, '4': 4, '5': 5, '6': 6 }
```

使用 ES6 提供的 map 方法

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function (nums) {
  let len = nums.length;
  let map = new Map();
  for (let i = 0; i < len; i++) {
    if (map.has(nums[i])) {
      return true;
    } else {
      map.set(nums[i], nums[i])
    }
  }
  return false;
};
```

### 巧用 Set

> `Set` can only store unique values. So if `Set.size` is less than `nums.length` - there have been duplicates.

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function (nums) {
  return (new Set(nums).size !== nums.length);
};
```

