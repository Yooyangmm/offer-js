# 剑指 Offer 06. 从尾到头打印链表

Easy

### 题目：

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

#### 示例1：

```js
输入：head = [1,3,2]
输出：[2,3,1]
```



### 解答：

#### 解法一：辅助数组

​	遍历链表，依次插入到辅助数组的头部。

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {number[]}
 */
var reversePrint = function(head) {
    const res = []
    while(head) {
        res.unshift(head.val)
        head = head.next
    }
    return res
};
```

#### 解法二：递归

​	通过递归遍历到链表底部，再从底部遍历回来，将每一个链表的val插入到数组中。

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {number[]}
 */
var reversePrint = function(head) {
    const res = []
    dfs(head, res)
    return res
};

function dfs(head, list) {
    if (!head) {
        return
    }
    dfs(head.next, list)
    list.push(head.val)
}
```

