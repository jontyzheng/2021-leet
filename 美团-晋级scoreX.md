[TOC]

### 原题

[1]: https://www.nowcoder.com/questionTerminal/31a1d7926cd947cc907de60ba8192b6c "题源牛客网"



题目描述：

小团是某综艺节目的策划，他为某个游戏环节设计了一种晋级规则，已知在这个游戏环节中每个人最后都会得到一个分数score_i，显而易见的是，游戏很有可能出现同分的情况，小团计划该环节晋级人数为x人，则将所有人的分数从高到低排序，所有分数大于等于第x个人的分数且得分不为0的人都可以晋级。

请你求出本环节的实际晋级人数。显然这个数字可能是0，如果所有人的得分都是0，则没有人满足晋级条件。

**输入描述:**

> 输入第一行包含两个正整数n和x，分别表示参加本环节的人数，和小团指定的x。输入第二行包含n个整数，每个整数表示一位选手的得分。

**输出描述:**

> 输出仅包含一个整数，表示实际晋级人数。

示例1

**输入**

```
5 4 
0 0 2 3 4
```

**输出**

```
3
```



### 题目分析

本题的难度不高，主要作为记录所用，所以不会涉及长篇的详解，只点出 2 个较为易错的点。

易错信息在题解的注释里。

1.题目描述中找的是位于降序序列中的第 n 个元素，也可以等价换算成升序序列中的第 xx 个，从而省略排序方法。

2.题目中的示例带有误导性，要是再加上下方注释中的用例就清晰多了



### 程序

```java
import java.util.*;

/**
 * @name  ScoresX
 * @what	https://www.nowcoder.com/questionTerminal/31a1d7926cd947cc907de60ba8192b6c
 * @do	通过
 * 题目有一个隐含的点在，目标分数是大于位于第 x 个位置上的分数的分数，以降序第 x 位上的分数值作为判断标准而不是第 x 个至前不为 0 的分数
 * 如果没有注意到这个，很有可能会出现少算的分数值
 * 1 2 3 4 5 5 6 7 8 (x=4) 结果为 5
 * */
public class ScoresX {
    public static void main(String[] args) {
        Scanner sn = new Scanner(System.in);
        int n = sn.nextInt();
        int x = sn.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = sn.nextInt();
        }
        Arrays.sort(arr);
        //先将数组升序，后从后往前找
        int cnt = 0;        
        int line = arr[n-x];
        //作为倒序，顺序第 x 个从反方向起是第 n-x+1 个，由于是数组，所以减去 1 表示当前的元素
        for (int i = n-1; i > 0; i--) {
            if (arr[i] >= line)
                cnt++;
            else
                break;
            //点到为止
        }
        System.out.println(cnt);
    }                
}
```

