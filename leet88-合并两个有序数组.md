# leet[88. 合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

[TOC]

### 一.原题

给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。

初始化 nums1 和 nums2 的元素数量分别为 m 和 n 。你可以假设 nums1 的空间大小等于 m + n，这样它就有足够的空间保存来自 nums2 的元素。

 

示例 1：

```
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]
```

示例 2：

```
输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]
```


提示：

- nums1.length == m + n
- nums2.length == n
- 0 <= m, n <= 200
- 1 <= m + n <= 200
- -109 <= nums1[i], nums2[i] <= 109



### 二.题要

有 2 个分别排好序的数组, 现在要把第二个数组中的元素插入到第一个数组后变成另一个重新排好序的数组.

已知, 第一个数组的长度是够的. 刚好满足 2 个数组的长度. 它们各自的元素个数也给出了. `m` 和 `n`.



### 三.理解

把第二个数组塞到第一个数组里, 然后对第一个数组排序.



#### 四.解

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        for (int i = m, j = 0; i < m+n; i++, j++) {
            nums1[i] = nums2[j];
        }
        Arrays.sort(nums1);
    }
}
```

1ms 22.52% 的水平



### 五.认识自己

看见 8 个月前 11 次提交记录, 也算是进步吧. 这次的一次提交.

  