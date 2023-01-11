# 剑指Offer17.打印从1到最大的n位数

Easy

### 题目：

​	输入数字 `n`，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

#### 示例1：

```
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```



### 解答：

#### 解法：JavaScript一行搞定

​	生成一个长度为 $$10^n$$ -1 的数组，设置初始值为1（必须），调用Array.map方法给设置每个值为 index + 1

```js
/**
 * @param {number} n
 * @return {number[]}
 */
var printNumbers = function(n) {
    return new Array(Math.pow(10, n) - 1).fill(1).map((item, index) => index + 1)
};
```

