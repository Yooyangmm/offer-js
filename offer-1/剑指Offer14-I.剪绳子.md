# 剑指Offer14-I.剪绳子

### 题目：

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

#### 示例1：

```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

#### 示例2：

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```



### 解答：

#### 解法一：动态规划

学习了[剪绳子题解](https://leetcode.cn/problems/jian-sheng-zi-lcof/solutions/100051/xiang-jie-bao-li-di-gui-ji-yi-hua-ji-zhu-dong-tai-/)的做法：

- 边界条件：`dp[1] = dp[2] = 1` 表示长度为 `2` 的绳子最大乘积为 `1`

- 状态转移方程：`dp[i] = max(dp[i], max((i - j) * j, j * dp[i - j]))`

<img src="images\14.png" alt="1672728632326" style="zoom: 100%;" />

```js
/**
 * @param {number} n
 * @return {number}
 */
var cuttingRope = function(n) {
    const dp = new Array(n + 1).fill(1)
    for (let i = 3; i <= n; i++) {
        for (let j = 1; j < i; j ++) {
            dp [i] = Math.max(dp[i], Math.max(j * (i - j), j * dp[i-j]))
        }
    }
    return dp[n]
};
```

#### 解法二：找规律 / 贪心

总结规律可知，只要尽可能的多分出长度为 `3` 的绳子，就能使得结果最大。

记分出的 `3` 的个数为 `a` ，得到的余数 `b` 只能是0，1，2

- b = 0：返回3的a次方 `Math.pow(3, a)`
- b = 1：把最后的一段的 `3 + 1` 拆分成 `2 + 2` ，返回 `Math.pow(3, a - 1) * 4`
- b = 2：返回 `Math.pow(3, a) * 2`

```js
/**
 * @param {number} n
 * @return {number}
 */
var cuttingRope = function(n) {
    if (n < 4) return n - 1
    let a = Math.floor(n / 3)
    let b = n % 3
    if (b === 0) {
        return Math.pow(3, a)
    } else if (b === 1) {
        return Math.pow(3, a - 1) * 4
    } else {
        return Math.pow(3, a) * 2
    }
};
```

