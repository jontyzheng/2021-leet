# other-水仙花数

### 一.概念

水仙花数（Narcissistic number）

也被称为超完全数字不变数（pluperfect digital invariant, PPDI）、自恋数、自幂数、阿姆斯壮数或阿姆斯特朗数（Armstrong number），

水仙花数是指一个 3 位数，

它的每个位上的数字的 3次幂之和等于它本身（例如：1^3 + 5^3+ 3^3 = 153）。

[摘自百度百科]

给定一大一小 2 个整数作为一个整数区间, 求这个整数区间内的水仙花数.





### 二.题解

#### 刀削面法

把一个数各个位数上的数字一个个削下来, 计算三次方然后累加起来, 最后和原来的数字对比.



##### 过程中可能会遇到的问题

- 如何将一个比如三位数, 把各个位数上的数字拿下来.

余十除十法:

以 125 举例, 先将 125 余十, 得到的就是 5. 这样, 每次作余十运算, 总能得到个位数, 也就是不能被 10 整除的数字.

接着, 将 125 除以十. 也就是缩小十倍, 剔除个位, 得到 25. 这样, 每次对十做除法, 总能剔除掉十位数. 得到剩余的位数上的数字.



### 三.代码实现(Java)

```java
package leet.calc;

import java.util.ArrayList;
import java.util.List;

/**
 * @name  FlowerNumber
 * @layer leet.calc
 * @intro
 * @function
 * */
public class FlowerNumber {
	public static List<Integer> findFlower(int n, int m) {
		List<Integer> list = new ArrayList<Integer>();
		
		for (int i = n; i <= m; i++) {
			int temp = i;	//	取出 i
			int res = 0;
			while (temp > 0) {
				int val = temp%10;
				double tVal = Math.pow(val, 3);
				res += tVal;	//整数的指数还是整数, 所以不影响结果
				temp/=10;
			}
			if (res == (int)i) {
				list.add(i);
			}
		}
		return list;
	}
	public static void main(String[] args) {
		int n = 152;
		int m = 500;
		System.out.println(findFlower(n, m));
        //[153, 370, 371, 407]
	}
}
```

另外, 如果题目要求返回一个整型数组的话, 分享一个冷门的方法.

```java
int[] a = list.stream().mapToInt(Integer::intValue).toArray();
```



