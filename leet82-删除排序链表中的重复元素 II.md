# leet[82. 删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)



#### 一.题目

存在一个按升序排列的链表，给你这个链表的头节点 head ，请你删除链表中所有存在数字重复情况的节点，只保留原始链表中 没有重复出现 的数字。

返回同样按升序排列的结果链表。

 

**示例 1：**

<img src="D:\桌面传送\markdown文档收录\leet100\linkedlist1.jpg" style="zoom:50%;" />

```
输入：head = [1,2,3,3,4,4,5]
输出：[1,2,5]
```

**示例 2：**

<img src="D:\桌面传送\markdown文档收录\leet100\linkedlist2.jpg" style="zoom:50%;" />

```
输入：head = [1,1,1,2,3]
输出：[2,3]
```

**提示：**

- 链表中节点数目在范围 `[0, 300]` 内
- `-100 <= Node.val <= 100`
- 题目数据保证链表已经按升序排列



#### 二.题要

已知值相同的结点总是挨在一起的, 要删除所有重复的节点, 包括节点本身.

最后保留只出现了一次的结点,



#### 三.分析

1.如果给定的链表结点个数为 0 或者个数为 1 则不存在重复的情形.

```java
if (head == null || head.next == null)
    return head;
```

2.第 1 种情形: 开头第一个开始就有重复

```
输入: 1, 1, 1, 2, 3
输出:	2,3
```

3.第 2 种情形: 

```
输入: 1, 2, 2, 2, 3
输出: 1, 3
```





#### 四.解

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null)
            return head;
        
        ListNode next = head.next;

        if (next.val == head.val) {
			//1
            while (next != null && next.val == head.val)
                next = next.next;
            head = deleteDuplicates(next);
        }
        else 
            head.next = deleteDuplicates(next);
        return head;
    }
}
```



##### 不理解的地方

1.已知 `next.val == head.val` (头结点后面还有和头节点值相等的结点)

那么不是默认 next 不为空了吗. 但是下一步检查的时候检查的还是 `while(next != null)`

下一个结点的下一个结点不应该是 `next.next` 吗



#### 五.认识链表

链表常用递归

