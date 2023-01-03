# 剑指 Offer 10- I. 斐波那契数列

### 题目：

写一个函数，输入 `n` ，求斐波那契（Fibonacci）数列的第 `n` 项（即 `F(N)`）。斐波那契数列的定义如下：

```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```

斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

#### 示例1：

```
输入：n = 2
输出：1
```

#### 示例2：

```
输入：n = 5
输出：5
```



### 解答：

#### 解法一：动态规划/滚动数组

1. 维护两个常量：`p` 、`q` 
2. 循环 `n - 1` 次，不断更新 `p = q` ；`q = p + q` （别忘记取模）

```js
/**
 * @param {number} n
 * @return {number}
 */
var fib = function(n) {
    if (n === 0) {
        return 0
    }
    let p = 0, q = 1
    while (--n) { // 循环 n-1次
        const tmp = p
        p = q
        q = (tmp + p) % 1000000007
    }
    return q
}
```

#### 解法二：矩阵快速幂

<img src="images\1672726838134.png" alt="1672728632326" style="zoom: 100%;" />

因此，令

<img src="images\1672728632326.png" alt="1672728632326" style="zoom: 5%;" />

因此只要快速计算矩阵 `M` 的 `n` 次幂，就可以得到 `F(n)` 的值。

定义矩阵乘法，然后用**快速幂算法**来加速计算矩阵 `M` 的 `n` 次幂。

```js
/**
 * @param {number} n
 * @return {number}
 */
var fib = function(n) {
    if (n < 2) return n
    const M = [[1, 1], [1, 0]]
    const res = pow(M, n - 1)
    return res[0][0]
}

const pow = (M, n) => { // 快速幂算法
    let ret = [[1, 0], [0, 1]] // 斐波那契数列的初始值
    while(n) {
        if (n & 1 === 1) { // 当n是奇数，多计算一次和M的矩阵相乘
            ret = multiply(ret, M)
        }
        n >>= 1 // 右移一位，相当于转换为二进制后再删除最后一位
        M = multiply(M, M)
    }
    return ret
}

const multiply = (A, B) => { // 两个 2x2 的矩阵相乘，结果仍是一个 2x2 矩阵
    const C = [[0, 0], [0, 0]]
    C[0][0] = (BigInt(A[0][0]) * BigInt(B[0][0]) + BigInt(A[0][1]) * BigInt(B[1][0])) % BigInt(1000000007)
    C[0][1] = (BigInt(A[0][0]) * BigInt(B[0][1]) + BigInt(A[0][1]) * BigInt(B[1][1])) % BigInt(1000000007)
    C[1][0] = (BigInt(A[1][0]) * BigInt(B[0][0]) + BigInt(A[1][1]) * BigInt(B[1][0])) % BigInt(1000000007)
    C[1][1] = (BigInt(A[1][0]) * BigInt(B[0][1]) + BigInt(A[1][1]) * BigInt(B[1][1])) % BigInt(1000000007)
    return C
}
```

