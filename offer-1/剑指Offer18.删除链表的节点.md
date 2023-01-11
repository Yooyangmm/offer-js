# 剑指Offer18.删除链表的节点

### 题目：

​	给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

#### 示例1：

```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```

#### 示例2：

```
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```



### 解答：

#### 解法一：双指针

- ​	用双指针 `l` 、 `r` 分别指向第一个节点和第二个节点，遍历整个链表，一旦找出要删除的元素，就进行  `l.next = r.next` 操作，即将 `r` 所指向节点的后一个节点（即 `r.next` ）拼接到 `l` 所指向的节点后面去；
- ​    如果当前元素不是要找的元素，就更新 `l` 和 `r` 两个指针，使他们分别往后移动一位。
- ​	直到当 `r` 所指向的节点为空为止。

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
 * @param {number} val
 * @return {ListNode}
 */
var deleteNode = function(head, val) {
    if (!head) return null
    if (head.val === val) return head.next
    let l = head, r = head.next
    while (r) {
        if (r.val === val) {
            l.next = r.next
        }
        l = l.next
        r = l ? l.next : null
    }
    return head
};
```

#### 解法二：单指针

​	总体思路会更简单一点

- ​	首先遍历链表，找出要删除的节点的前一个节点，用指针 `cur` 指向它；
- ​	对该节点 `cur` 执行 `cur.next = cur.next.next` 操作，即将 `cur` 后的第二个节点接到 `cur` 后面去。

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
 * @param {number} val
 * @return {ListNode}
 */
var deleteNode = function(head, val) {
    if (!head) return null
    if (head.val === val) return head.next
    let cur = head
    while(cur.next && cur.next.val !== val) {
        cur = cur.next
    }
    cur.next = cur.next.next
    return head
};
```

