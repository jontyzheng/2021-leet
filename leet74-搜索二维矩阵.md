# leet[74. 搜索二维矩阵](https://leetcode-cn.com/problems/search-a-2d-matrix/)

[TOC]

#### 一.题目

编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

每行中的整数从左到右按升序排列。
每行的第一个整数大于前一行的最后一个整数。


示例 1：

![](D:\桌面传送\markdown文档收录\leet100\img\mat.jpg)[]

```
输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
输出：true
```

**示例 2：**

![](D:\桌面传送\markdown文档收录\leet100\img\mat2.jpg)

```
输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
输出：false
```

提示：

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 100
- -104 <= matrix[i][j], target <= 104



#### 二.题要

已知矩阵是按照从小到大顺序依次排好的, 写一个方法查找内部是否含有这个值.



#### 三.理解

1.数字都是按照从小到大的顺序排好的, 那么根据扁平化的思想, 将值一个个装起来, 然后线性查找.

2.因为数值都是排列好的, 所以如果匹配到, 就返回 `true` 结束. 如果对比到更大的值时就不用继续往后寻找了.



四.解

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        List<Integer> list = listed(matrix);
        for (int i = 0 ; i < list.size(); i++) {
            if (list.get(i) == target) {
                return true;
            }
            else if (list.get(i) > target) {
                return false;
            }
        }
        return false;
    }

    public List<Integer> listed(int[][] matrix) {
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length; j++) {
                list.add(matrix[i][j]);
            }
        }
        return list;
    }
}
```

2 ms, 内存 38.2 MB



#### 五.认识查找

1.扁平化的运用

2.有序数组线性查找的应用