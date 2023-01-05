# 剑指Offer12.矩阵中的路径

### 题目：

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。

<img src="images\word2.jpg" alt="1672728632326" style="zoom: 100%;" />

#### 示例1：

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

#### 示例2：

```
输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false
```



### 解答：

#### 解法：dfs

初始化：

​	 `i` 和 `j` ：当前元素在矩阵 `board` 中的索引值

​	`k` ：当前目标字符在 `word` 中的索引

dfs思路：

1. 递归出口：

   索引值越界 或 当前元素和word元素不同，说明该路径无法正常访问，返回 `false` ；

   字符串word已经全部匹配成功时，返回 `true`

 2. 递归主体：

    1. 当前元素 `board[i][j] `与 `word[k]` 相同，说明当前元素匹配成功

    2. 将当前 `board[i][j] ` 置为空（避免重复访问该元素）

    3. 继续往上下左右四个方向扩散

    4. 将 `board[i][j]` 元素还原至初始值，即 `word[k]`

两层循环对每个元素执行dfs即可~

```js
/**
 * @param {character[][]} board
 * @param {string} word
 * @return {boolean}
 */
var exist = function(board, word) {
    for (let i = 0; i < board.length; i++) {
        for (let j = 0; j < board[0].length; j++) {
            if (dfs(board, word, i, j, 0)) {
                return true
            }
        }
    }
    return false
}
const dfs = (board, word, i, j, k) => {
    if (i >= board.length || i < 0 || j >= board[0].length || j < 0 || board[i][j] !== word[k]) {
        return false
    }
    if (k === word.length - 1) {
        return true
    }
    board[i][j] = '' // 修改board[i][j]为空，代表该元素已经访问过了，避免重复访问
    const res = dfs(board, word, i + 1, j, k + 1) || dfs(board, word, i - 1, j, k + 1) ||
                dfs(board, word, i, j + 1, k + 1) || dfs(board, word, i, j - 1, k + 1)
    board[i][j] = word[k] // 将board[i][j]还原为初始值
    return res
}
```

