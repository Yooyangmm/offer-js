# 剑指Offer07.重建二叉树

Medium

### 题目：

输入某二叉树的前序遍历和中序遍历的结果，请构建该二叉树并返回其根节点。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

#### 示例1：

![image-20230103112634249](images\image-20230103112634249.png)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

#### 示例2：

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```



### 解答：

#### 解法一：递归

前序遍历：根 左 右

中序遍历：左 根 右

​	根据这两种遍历结果的特性可以知道，可以在前序队列preorder中取出首元素后，在中序队列inorder中以该元素分隔成 `[[左子树], root, [右子树]]`

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function(preorder, inorder) {
    if (!preorder.length || !inorder.length) {
        return null
    }
    const rootValue = preorder.shift() // 获取当前根节点的值，并将其从前序遍历preorder中删除
    const rootIndexOfInorder = inorder.indexOf(rootValue) // 当前根节点在中序遍历inorder中的位置
    const root = new TreeNode(rootValue) // 创建根节点
    root.left = buildTree(preorder, inorder.slice(0, rootIndexOfInorder)) // 取inorder左半段继续生成左子节点
    root.right = buildTree(preorder, inorder.slice(rootIndexOfInorder + 1)) // 取inorder右半段继续生成右子节点
    return root
};
```



