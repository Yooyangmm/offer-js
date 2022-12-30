# 剑指Offer04.二维数组中的查找

Medium

### 题目：

​	在一个 n * m 的二维数组中，每一行都按照从左到右 非递减 的顺序排序，每一列都按照从上到下 非递减 的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

##### **示例:**

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。



### 解答：

#### 解法一：暴力

​	数组扁平化后直接查找

```js
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var findNumberIn2DArray = function(matrix, target) {
    return matrix.flat().includes(target)
};
```

#### 解法二：

​	题干中说到：`每一行都按照从左到右非递减的顺序排序，每一列都按照从上到下非递减的顺序排序` 。因此我们将二维数组向左旋转45度后，这个二维数组可以看成一个二叉排序树（每一个节点的左子节点都小于该节点，每一个节点的右子节点都大于该节点），因此我们可以直接从右上角的元素x开始，和 `target` 比较：若相等则说明找到了；若 `x > target`，则向右子树找；否则就向左子树找。

![image-20221230151657345](C:\Users\杨杨\AppData\Roaming\Typora\typora-user-images\image-20221230151657345.png)

```js
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var findNumberIn2DArray = function(matrix, target) {
    const n = matrix.length
    if (!n) return false
    const m = matrix[0].length
    let i = 0, j = m - 1
    while (i < n && j >= 0) {
        if (matrix[i][j] === target) {
            return true
        } else if (matrix[i][j] > target) {
            j--
        } else {
            i++
        }
    }
    return false
};
```



















