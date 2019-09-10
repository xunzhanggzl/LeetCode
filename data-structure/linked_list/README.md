## 2. 两数相加

[2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例:

`输入：(2 -> 4 -> 3) + (5 -> 6 -> 4) 。输出：7 -> 0 -> 8 。原因：342 + 465 = 807`

## 链表

充分利用  `&&`  和 `三目运算符` 的功能，这里先建立一个空的链表头，最后返回的是列表头的 next。

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function (l1, l2) {
  let result = new ListNode();
  let listnode = result;
  let c = 0; 
  while (l1 || l2 || c) {
    let val1 = l1 ? l1.val : 0;
    let val2 = l2 ? l2.val : 0;
    let val = val1 + val2 + c;
    listnode.next = new ListNode(val % 10);
    listnode = listnode.next;
    c = val >= 10 ? 1 : 0;
    l1 = l1 && l1.next;
    l2 = l2 && l2.next;
  }
  console.log(result);  // 下面是打印的 result 的结果。
  return result.next;
};
```

这是 `result` 的结果。

```javascript
ListNode {
  val: undefined,
  next:
   ListNode { val: 7, next: ListNode { val: 0, next: [ListNode] } } }
```
