## 118.杨辉三角

[118. 杨辉三角](https://leetcode-cn.com/problems/pascals-triangle/)

给定一个非负整数 *numRows，*生成杨辉三角的前 *numRows* 行。

### 递归

```javascript
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function (numRows) {
  if (numRows === 1) {
    return [[1]]
  } else if (numRows === 2) {
    return [[1],[1, 1]]
  } else if (numRows === 0) {
    return [];
  } else {
    let result = [[1],[1, 1]];
    for (let i = 3; i <= numRows; i++) {
      let arr = [];
      arr.push(1); 
      for (let j = 1; j <= i - 2; j++) {
        arr[j] = result[i - 2][j - 1] +
          result[i - 2][j];
      }
      arr.push(1);
      result.push(arr);
    }
    return result;
  }
};
```

