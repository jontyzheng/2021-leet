# leet[341. 扁平化嵌套列表迭代器](https://leetcode-cn.com/problems/flatten-nested-list-iterator/)

[TOC]

#### 一.题目

```
给你一个嵌套的整型列表。请你设计一个迭代器，使其能够遍历这个整型列表中的所有整数。

列表中的每一项或者为一个整数，或者是另一个列表。其中列表的元素也可能是整数或是其他列表。

 

示例 1:

输入: [[1,1],2,[1,1]]
输出: [1,1,2,1,1]
解释: 通过重复调用 next 直到 hasNext 返回 false，next 返回的元素的顺序应该是: [1,1,2,1,1]。
示例 2:

输入: [1,[4,[6]]]
输出: [1,4,6]
解释: 通过重复调用 next 直到 hasNext 返回 false，next 返回的元素的顺序应该是: [1,4,6]。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/flatten-nested-list-iterator
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



#### 二.题要

有一个列表, 它的每一项又是一个列表, 长度各不相同.

想要写一个迭代器把里面的元素从头到尾依次输出来.



##### 提示

###### a.自带的类

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
```

这一个类是给定的代表每一项的类.

三个方法分别是:

```
1.判断项是不是一个整数 isInteger():boolean
2.是整数时	getInteger():int
3.是小列表时	getList():List<NestedInteger>
```



###### b.迭代器类的构造器参数

```java
public NestedIterator(List<NestedInteger> nestedList) {
        
}
```



这个迭代器类是要实例化就能拿来获取对应元素的. 本身要包含目标列表.

所以应该缺一个内置的列表属性. (构造器传参初始化也是一个提示).



###### c.方法

```
1.next(): Integer	//返回下一项
2.hasNext(): boolean	//判断是否遍历完 暗示缺一个计数器 
```



#### 三.分析

一个列表 list 有 get(i) 以及 size() 方法, 如果获取内部的项的接口也知道了.

只差一个把所有元素都装进一个 list 的方法.



#### 四.解

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class NestedIterator implements Iterator<Integer> {

    private List<Integer> list = new ArrayList<>();
    private int index;

    public void add(List<NestedInteger> nestedList) {
        for (NestedInteger i : nestedList) {
            if (i.isInteger()) {
                list.add(i.getInteger());
            }
            else {
                add(i.getList());	//*(迭代 | 判断并添加)
            }
        }
    }
    //精炼小结: 是整数就 getInteger(), 是列表就 getList()

    public NestedIterator(List<NestedInteger> nestedList) {
        add(nestedList);
    }

    @Override
    public Integer next() {
        return list.get(index++);        //*
    }    

    @Override
    public boolean hasNext() {
        return index < list.size();
    }
}

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i = new NestedIterator(nestedList);
 * while (i.hasNext()) v[f()] = i.next();
 */
```

执行时间 3 ms, 内存消耗 41 MB



#### 五.实验分析

把长短不一的列表从头到尾一个个装进另一个列表里.



#### 六.认识递归

1.`NestedInteger` 表示列表的项. 可以是一个 `Integer` , 还可以是一个 `List<Integer>`

2.我们知道的是如果是 `Integer` 时怎么获取, 如果是一个 `List<NestedInteger>` 时怎么获取.

但是拿到 列表项(如果的话) 也是要继续判断最后拿到 `Integer` 的. 但是一个列表项只会有一次.

对返回的项重复相同的逻辑, 用递归(`add` 方法)

参考: https://leetcode-cn.com/problems/flatten-nested-list-iterator/comments/4898



##### 为什么叫做扁平化

因为迭代器是将这个不规则链表每一项遍历并添加到一个一维的列表中, 相当于将一个二维的数据拉升成了一维的数据.

##### 怎么实现扁平的

检查到 `NestedInteger` 是一个整数的时候, 添加到 `list` 当中;

当检查到 `NestedInteger` 是一个列表的时候, 迭代重复方法.