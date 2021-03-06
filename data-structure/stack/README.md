## 20. 有效的括号

[20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。左括号必须以正确的顺序闭合。注意空字符串可被认为是有效字符串。

**示例 1:**

```
输入: "()"
输出: true
```

**示例 2:**

```
输入: "()[]{}"
输出: true
```

**示例 3:**

```
输入: "(]"
输出: false
```

### Stack

如果  `s.length`  是奇数，直接返回  `false`  提高效率

利用栈的原理，使用 `for of` 代替 `for` 循环来遍历字符串，非常简便。

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */    
const obj = {
  "(": ")",
  "{": "}",
  "[": "]"
}
var isValid = function (s) {
  if (s.length % 2 !== 0) {
    return false;
  }
  let stack = [];
  for (let c of s) {
    if (c in obj) {
      stack.push(obj[c]);
    } else {
      if (c !== stack.pop()) {
        return false;            
      }
    }
  }
  return stack.length === 0;
}
```