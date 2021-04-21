特殊二维数组中的查找简述

#### 题目

有这么一个二维数组

```
每一行都按照从左到右递增的顺序排序, 每一列都按照从上到下递增的顺序排序.
```

写出一个函数, 输入这么一个二维数组和整数, 判断该数组中是否含该数字.

例如

```
1	2	8	9
2	4	9	10 
4 	7	10	13
6 	8 	11 	15
```

####  分析

已知数据在每一行和每一列都是按照升序排列的

以 7 为例, 如果目标数字比 7 大的话, 那么总是落在 7 的右上, 右下, 或者左下区域.

```
		8	9
		9	10 
		10	13
6 	8 	11 	15	
```

以 10 为例, 如果目标数组比 10 小的话, 那么总是落在 10 的左上, 右上, 或者左下区域.

```
1	2	8	9
2	4	9	10
4 	7	
6 	8 
```

可以发现, 总是能排除以比较位置为基准的一个角的区域. 那么是左上方发散出去, 那么是右下方发散出去.

唯一的问题是数字落在的区域有重叠. 

这里有一个技巧. 从数组的一个角选取数字来和要查找的数字作比较, 情况就会变简单.

```
首先, 拿数组右上角的 9 作比较. 因为 9 比 7 大, 并且 9 是列中最小的数字也是最靠右边的数字
所以 7 不可能出现在 9 所在的列, 从而剔除了第 4 列.
接着, 拿 8 作比较.
由于 8 比 7 大, 同理可能, 7 也不可能出现在 8 所在的列.
所以又可以剔除掉第 3 列.
接着, 拿 2 作比较
由于 7 比 2 大, 2 又是第一行最后一个
不可能在 2 的左边, 所以又剔除了第一行.
那么只剩下三行两列的数字.

此时, 4 位于右上角,
前面的一样, 和 4 比较完后, 又剔除第二行. 剩下两行两列.

而在剩下的两行两列中, 右上角的 7 正好是要查找的数字.
```

2021-04-07 21:55:31



作图

 <img src="D:\桌面传送\markdown文档收录\leet100\img\matrix-select.png" style="zoom: 15%;" />

大小区域分布的区域呈现成一个"回车键"的形状.



了解了整个查找的技巧之后, 我们再写代码就不是一件十分很难的事情了.

```java
package leet.arr;

/**
 * @name  SelectFromMatrix
 * @layer leet.arr
 * @intro
 * @function
 * */
public class SelectFromMatrix {
	public static boolean find(int[][] matrix, int rows, int cols, int number) {
		boolean findFlag = false;
		if (matrix.length != 0 && cols > 0 && rows > 0) {
			int row = 0;
			int col = cols - 1;	
			//使初始值等于右上角的值
			while (row < rows && col >= 0) {
				//对比之后如果目标值比比较相等, 那么匹配成功
				if (matrix[row][col] == number) {
					findFlag = true;
					break;
				}
				//对比之后如果目标值比比较值更小, 那么值落在左边的enter区域, 减去右边就是左边区域
				else if (matrix[row][col] > number)
					//修改col往左继续查找
					--col;
				//对比之后如果目标值比比较值更大, 那么值落在右下角的enter区域, 减去左边和右边就只有下边区域
				else
					++row;						
			}
		}
		return findFlag;
	}
	
	public static void main(String[] args) {
		int[][] a = {{1,2,8,9}, {2,4,9,12}, {4,7,10,13}, {6,8,11,15}};
		int rows = a.length;
		int cols = a[0].length;
		int target = 9;
		boolean hasTarget = find(a, rows, cols, target);
		System.out.println(hasTarget);
	}
}

```

2021-04-07 21:12:04



参考: 剑指 offer  第 2 章面试需要的基础知识 面试题三: 二维数组中的查找