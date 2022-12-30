# 剑指 Offer 03. 数组中重复的数字

### 题目：

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

**示例 1：**

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```



### 解答：

#### 解法一：遍历数组，Set存储

​	遍历数组，每次判断当前 `nums[i]` 是否在 `set` 中出现过：若出现过，则说明找到重复数字；反之，将该 `nums[i]` 添加到 `set` 中。

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findRepeatNumber = function(nums) {
    const set = new Set()
    for (let i = 0; i < nums.length; i++) {
        if (set.has(nums[i])) {
            return nums[i]
        } else {
            set.add(nums[i])
        }
    }
    return -1
};
```

#### 解法二：原地交换

​	注意题干说 `在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内` ，说明数组元素的索引和值是**一对多**的关系！因此只需要遍历数组并通过交换操作，使元素的**索引**与**值** 一一对应，即 `nums[i]===i` ，

​	简单来说就是：遍历数组，如果当前位置放元素的索引和值相同，则往下遍历。否则，遇到4就把4放到索引为4的地方，但如果这个时候4的地方已经放的是4了，则说明多了一个4，即找出了重复数字4。

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findRepeatNumber = function(nums) {
    let i = 0
    while (i < nums.length) {
        if (nums[i] === i) {
            i++
            continue
        }
        if (nums[i] === nums[nums[i]]) {
            return nums[i]
        }
        const tmp = nums[i] // 将nums[i]和nums[nums[i]]交换
        nums[i] = nums[tmp]
        nums[tmp] = tmp
    }
    return -1
};
```

