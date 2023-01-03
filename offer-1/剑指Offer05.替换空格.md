# 剑指Offer05.替换空格

Easy

### 题目：

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

#### 示例 1：

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

### 解答：

#### 解法一：replaceAll

```js
/**
 * @param {string} s
 * @return {string}
 */
var replaceSpace = function(s) {
    return s.replaceAll(' ', '%20')
};
```

#### 解法二：正则

```js
/**
 * @param {string} s
 * @return {string}
 */
var replaceSpace = function(s) {
    return s.replace(/[ ]/g, '%20')
};
```

