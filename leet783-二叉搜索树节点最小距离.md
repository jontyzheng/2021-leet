# leet[783. 二叉搜索树节点最小距离](https://leetcode-cn.com/problems/minimum-distance-between-bst-nodes/)



一.原题

给你一个二叉搜索树的根节点 root ，返回 树中任意两不同节点值之间的最小差值 。

注意：本题与 530：https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/ 相同

 

示例 1：

<img src="D:\桌面传送\markdown文档收录\leet100\img\bst1.jpg" style="zoom: 50%;" />

```
输入：root = [4,2,6,1,3]
输出：1
```




示例 2：

<img src="D:\桌面传送\markdown文档收录\leet100\img\bst2.jpg" style="zoom:50%;" />

```
输入：root = [1,0,48,null,null,12,49]
输出：1
```




提示：

- 树中节点数目在范围 [2, 100] 内
- 0 <= Node.val <= 10



二.解

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
class Solution {
    private TreeNode pre = null;    
    private int res = Integer.MAX_VALUE;
    
    public int minDiffInBST(TreeNode root) {       
        dfs(root);
        return res;
    }

    private void dfs(TreeNode root) {
        if (root == null)
            return;
        dfs(root.left);
        if (pre !=null) {
            res = Math.min(root.val-pre.val, res);
        }
        
        pre = root;
        dfs(root.right);
    }
}
```

