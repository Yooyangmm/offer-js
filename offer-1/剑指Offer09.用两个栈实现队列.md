# 剑指 Offer 09. 用两个栈实现队列

### 题目：

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

#### 示例 1：

```js
输入：
["CQueue","appendTail","deleteHead","deleteHead","deleteHead"]
[[],[3],[],[],[]]
输出：[null,null,3,-1,-1]
```

#### 示例2：

```js
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```



### 解答：

**栈：后进先出**

**队列：先进先出**

思路：

1. 维护两个栈：

   `inStack` 只负责入队列

   `outStack` 只负责出队列

2. 入队列直接插入 `inStack`

3. 出队列则优先考虑从 `outStack` 中删去；如果 `outStack` 中没有元素了，则考虑将 `inStack` 中的所有元素插入 `outStack` 中，再从 `outStack` 中删去。

```js

const CQueue = function() {
    this.inStack = []
    this.outStack = []
}

/** 
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function(value) {
    this.inStack.push(value)
    return value
}

/**
 * @return {number}
 */
CQueue.prototype.deleteHead = function() {
    if (this.outStack.length) { // 如果outStack中仍存在逆序元素，直接pop
        return this.outStack.pop()
    }
    if (!this.inStack.length) { // 如果inStack和outStack都为空，说明队列中没有元素，返回-1
        return -1
    }
    while(this.inStack.length) { // 将inStack中的元素插入outStack
        this.outStack.push(this.inStack.pop())
    }
    return this.outStack.pop()
}

/**
 * Your CQueue object will be instantiated and called as such:
 * var obj = new CQueue()
 * obj.appendTail(value)
 * var param_2 = obj.deleteHead()
 */
```

