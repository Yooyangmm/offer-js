# 剑指Offer10-II.青蛙跳台阶问题

### 题目：

```js
一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。
```

#### 示例 1：

```
输入：n = 2
输出：2
```

#### 示例2：

```
输入：n = 7
输出：21
```

#### 示例3：

```
输入：n = 0
输出：1
```

### 解答：

​	记跳到第n个台阶的跳法为 `f(n)` ，由题意可知，青蛙每次可以跳1级或2级台阶。

​	所以青蛙要想跳到第n级台阶，只能从 `n-1` 或 `n-2` 跳。所以可知 `f(n) = f(n-1) + f(n-2)` ，和上一题的斐波那契数列原理相同，区别在于两者的起始值不同：斐波那契数列的起始值是 0 1 1 ... ；而青蛙跳水的起始值是 1 1 2 ...。

#### 解法一：动态规划

1. 维护两个常量：`p` 、`q` 

2. 循环 `n` 次，不断更新 `p = q` ；`q = p + q` （别忘记取模），多循环了一次，所以取了 `q` 的值

```js
/**
 * @param {number} n
 * @return {number}
 */
var numWays = function(n) {
    let p = 1, q = 1
    while (n--) { // 循环计算n次（其实多算了一次，但是可以不用判断边界值）
        const tmp = p
        p = q
        q = (tmp + p) % 1000000007
    }
    return p
}
```

#### 解法二：矩阵快速幂

这道题的思路和前一题相似，只需要改变一下初始值即可

[跳转题解 -- 剑指Offer10-I.斐波那契数列](https://github.com/Yooyangmm/offer-js/blob/master/offer-1/%E5%89%91%E6%8C%87Offer10-I.%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0%E5%88%97.md)

```js
/**
 * @param {number} n
 * @return {number}
 */
var numWays = function(n) {
    if (n < 2) return 1
    const M = [[1, 1], [1, 0]]
    const res = pow(M, n)
    return res[0][0]
}

const pow = (M, n) => {
    let ret = [[1, 0], [1, 1]] // 初始值
    while(n) {
        if (n & 1 === 1) {// n是奇数
            ret = multiple(ret, M)
        }
        n >>= 1
        M = multiple(M, M)
    }
    return ret
}

const multiple = (A, B) => { // 两个二维矩阵相乘，返回值是一个二维矩阵
    const C = [[0, 0], [0 , 0]]
    C[0][0] = (BigInt(A[0][0]) * BigInt(B[0][0]) + BigInt(A[0][1]) * BigInt(B[1][0])) % BigInt(1000000007)
    C[0][1] = (BigInt(A[0][0]) * BigInt(B[0][1]) + BigInt(A[0][1]) * BigInt(B[1][1])) % BigInt(1000000007)
    C[1][0] = (BigInt(A[1][0]) * BigInt(B[0][0]) + BigInt(A[1][1]) * BigInt(B[1][0])) % BigInt(1000000007)
    C[1][1] = (BigInt(A[1][0]) * BigInt(B[0][1]) + BigInt(A[1][1]) * BigInt(B[1][1])) % BigInt(1000000007)
    return C
}
```

