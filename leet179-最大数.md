# leet[179. 最大数](https://leetcode-cn.com/problems/largest-number/)



一.原题

给定一组非负整数 `nums`，重新排列每个数的顺序（每个数**不可拆分**）使之组成一个最大的整数。

注意：输出结果可能非常大，所以你需要返回一个字符串而不是整数。

 

示例 1：

```
输入：nums = [10,2]
输出："210"
```

示例 2：

```
输入：nums = [3,30,34,5,9]
输出："9534330"
```


示例 3：

```
输入：nums = [1]
输出："1"
```


示例 4：

```
输入：nums = [10]
输出："10"
```




提示：

- 1 <= nums.length <= 100
- 0 <= nums[i] <= 109



二.题要



三.信息

1.不可拆分, 注意是

题意

```
假如是 3,30,34,5,9
排序后应该是 9 5 34 33 3
```



四.解

```java
class Solution {
    public String largestNumber(int[] nums) {
        int n=nums.length;
        String numsToWord[]=new String[n];
        for(int i=0;i<n;i++)
        {
            numsToWord[i]=String.valueOf(nums[i]);//将数字转化成字符串
        }
        Arrays.sort(numsToWord,(a,b)->{
            return (b+a).compareTo(a+b);
        });
        //更改排序方法，如223，22比较是22322大还是22322大
        if(numsToWord[0].equals("0"))//若第一个字母为0则结果为0
        {
            return "0";
        }
        StringBuilder sb=new StringBuilder();
        for(int i=0;i<n;i++)
        {
            sb.append(numsToWord[i]);
        }
        return sb.toString();
    }

}
```

Arrays 的 sort 可以重写!



参考自 https://leetcode-cn.com/problems/largest-number/comments/886981