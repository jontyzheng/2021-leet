# leet[81. 搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)

#### 一.题目

已知存在一个按非降序排列的整数数组 `nums`，数组中的值不必互不相同。

在传递给函数之前，`nums` 在预先未知的某个下标 `k`（`0 <= k < nums.length`）上进行了 旋转 ，使数组变为 `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]`（下标 从 0 开始 计数）。例如， `[0,1,2,4,4,4,5,6,6,7]` 在下标` 5` 处经旋转后可能变为 `[4,5,6,6,7,0,1,2,4,4] `。

给你 旋转后 的数组 `nums` 和一个整数 `target` ，请你编写一个函数来判断给定的目标值是否存在于数组中。如果 `nums `中存在这个目标值 `target` ，则返回 `true `，否则返回 `false `。

 

示例 1：

```
输入：nums = [2,5,6,0,0,1,2], target = 0
输出：true
```

示例 2：

```
输入：nums = [2,5,6,0,0,1,2], target = 3
输出：false
```


提示：

- `1 <= nums.length <= 5000`
- `-104 <= nums[i] <= 104`
- 题目数据保证 `nums` 在预先未知的某个下标上进行了旋转
- `-104 <= target <= 104`





#### 二.题要

有一个数组, 它本来是排好序的, 只是要一个地方截取了一段, 然后把后半段给调到前面去了.

现在, 给你一个数字, 问它在不在这个数组中.



#### 三.理解

本质还是一个给值查找的问题, 可以线性查找.

或者, 排好序, 再用循环因子跳出法.



四.解

i.简单直接

```java
class Solution {
    public boolean search(int[] nums, int target) {
        boolean hasIt = false;
        for (int i = 0; i < nums.length; i++) {
            if (target == nums[i]) {
                hasIt = true;
                break;
            }
        }
        return hasIt;
    }
}
```

执行用时: **1 ms** 内存消耗: **38.1 MB**



ii.往出题人靠

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int n = nums.length;        
        Arrays.sort(nums);
        int z;
        for (z = 0; z < n; z++) {
            if (nums[z] == target)
                break;
        }
        return z < n;
    }
}
```

执行用时：2 ms, 在所有 Java 提交中击败了88.78%的用户



