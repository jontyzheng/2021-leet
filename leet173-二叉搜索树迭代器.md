# leet[173. 二叉搜索树迭代器](https://leetcode-cn.com/problems/binary-search-tree-iterator/)

[TOC]



#### 一.题目

```
实现一个二叉搜索树迭代器类BSTIterator ，表示一个按中序遍历二叉搜索树（BST）的迭代器：
BSTIterator(TreeNode root) 初始化 BSTIterator 类的一个对象。BST 的根节点 root 会作为构造函数的一部分给出。指针应初始化为一个不存在于 BST 中的数字，且该数字小于 BST 中的任何元素。
boolean hasNext() 如果向指针右侧遍历存在数字，则返回 true ；否则返回 false 。
int next()将指针向右移动，然后返回指针处的数字。
注意，指针初始化为一个不存在于 BST 中的数字，所以对 next() 的首次调用将返回 BST 中的最小元素。

你可以假设 next() 调用总是有效的，也就是说，当调用 next() 时，BST 的中序遍历中至少存在一个下一个数字。

```

**示例：**

![](D:\桌面传送\markdown文档收录\leet100\img\bst-tree.png)

```
输入
["BSTIterator", "next", "next", "hasNext", "next", "hasNext", "next", "hasNext", "next", "hasNext"]
[[[7, 3, 15, null, null, 9, 20]], [], [], [], [], [], [], [], [], []]
输出
[null, 3, 7, true, 9, true, 15, true, 20, false]

解释
BSTIterator bSTIterator = new BSTIterator([7, 3, 15, null, null, 9, 20]);
bSTIterator.next();    // 返回 3
bSTIterator.next();    // 返回 7
bSTIterator.hasNext(); // 返回 True
bSTIterator.next();    // 返回 9
bSTIterator.hasNext(); // 返回 True
bSTIterator.next();    // 返回 15
bSTIterator.hasNext(); // 返回 True
bSTIterator.next();    // 返回 20
bSTIterator.hasNext(); // 返回 False

```

提示：

    树中节点的数目在范围 [1, 105] 内
    0 <= Node.val <= 106
    最多调用 105 次 hasNext 和 next 操作


进阶：

你可以设计一个满足下述条件的解决方案吗？next() 和 hasNext() 操作均摊时间复杂度为 O(1) ，并使用 O(h) 内存。其中 h 是树的高度。



### 二.题要

现在有一个二叉树, 写一个功能类, 可以依次将其中的结点按"先序遍历"的顺序取出元素的类.

`next()` 可以拿到下一个结点的值

`hasNext()` 可以判断二叉树中还有没有没取出来的值.



(构造的意思: 传入二叉树根节点作为构造器的参数)





### 三.理解

**扁平化**: 前天遇到的遍历不规则链表数组也是扁平化, 也是链式结构, 也是 rank middle.

即将研究对象中的值存放到一个一维的列表容器里.

然后通过内置方法, 利用动态变化的计数器结合列表长度判断 是否有下一个元素, 取出下一个元素(这时候, 已经是当作列表按下标取出了)

##### 先序遍历

```
左孩 -> 根节点 -> 右孩
```

例子:

题目图片中的例子的结点遍历下来就是

```
[3, 7, 9, 15, 20]
```



##### 理清楚一个问题

##### 要对可递归元素的项做怎样重复的操作

```
1.判断是否为空	如果为空, 不做任何操作(是的, 不做任何操作也要写出来, 在递归中这样的条件还可能是一个方法结束的终点)
2.如果不为空, 将左节点做这样的操作 - 这时研究对象是左节点, 列表依然要作为参数传进入(全局属性)
3.如果左孩不为空, 继续检查左结点. 如果左节点的左节点传入为空, 不做任何操作 此时将左节点的值添加进列表(对应着二叉树最左下方的结点)
4.添加完后检查右结点, 也是要重复它的左节点
也就是说, 这些操作都要放在一个同级的程序中. 然后递归复用.
```



### 四.解

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class BSTIterator {

    private List<Integer> arr;
    private int index;
    //全局计数器, 每 next() 提取一次值就变化一次

    public BSTIterator(TreeNode root) {
        index = 0;
        arr = new ArrayList<Integer>();
        traverse(root, arr);
        //在调用构造器的时候完成列表内容的添加
    }
    
    public int next() {
        return arr.get(index++);
    }
    
    public boolean hasNext() {       
        return index < arr.size();
    }
    //检查计数器的值和列表长度之间的大小

    private void traverse(TreeNode root, List<Integer> arr) {
        if (root == null)
            return;            
        traverse(root.left, arr);
        arr.add(root.val);
        traverse(root.right, arr);
    }
    //传入根节点左结点作为 root 的时候等效于当前左节点为根节点
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```





### 五.理解二叉树先序遍历

1.先序遍历: 左-中-右