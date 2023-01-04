# 剑指Offer11.旋转数组的最小数字

### 题目：

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

给你一个可能存在 重复 元素值的数组 numbers ，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一次旋转，该数组的最小值为 1。  

注意，数组 [a[0], a[1], a[2], ..., a[n-1]] 旋转一次 的结果为数组 [a[n-1], a[0], a[1], a[2], ..., a[n-2]] 。

#### 示例1：

```
输入：numbers = [3,4,5,1,2]
输出：1
```

#### 示例2：

```
输入：numbers = [2,2,2,0,1]
输出：0
```

### 解答：

<img src="images\1221387183719247.png" alt="1672728632326" style="zoom: 100%;" />

#### 解法：二分法

首选声明双指针 `i, j` 分别指向 `nums` 数组左右两端

开始循环，设 `mid = i + Math.floor((j - i) / 2)` 为每次二分的中点，有以下三种情况：

1. 当 `nums[mid] > nums[j]` 时： `mid` 一定在左排序数组中，且由于 `nums[mid] > nums[j]` ，所以 `num[mid]` 不可能是最小值，因此执行 `i = mid + 1` 

2. 当 `nums[mid] < nums[j]` 时： `mid` 一定在右排序数组 中，因此执行 `j = mid` ；

3. 当 `nums[mid] = nums[j]` 时： 无法判断 `mid` 在左右区间内，所以执行 `j--` 缩小右区间。

   特殊情况如 `[1, 1, 0, 1]` 的数组，当 `nums[mid] = nums[j]` 时，无法通过直接二分来缩小范围，所以使用 `j--` 来缩小区间。

```js
/**
 * @param {number[]} numbers
 * @return {number}
 */
var minArray = function(numbers) {
    let i = 0, j = numbers.length - 1
    while (i < j) {
        const mid = i + Math.floor((j - i) / 2)
        if (numbers[mid] > numbers[j]) {
            i = mid + 1
        } else if (numbers[mid] < numbers[j]) {
            j = mid
        } else {
            j--
        }
    }
    return numbers[i]
};
```

