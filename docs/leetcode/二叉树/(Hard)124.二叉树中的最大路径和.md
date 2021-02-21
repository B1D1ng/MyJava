#### 题目
```
路径 被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。同一个节点在一条路径序列中 至多出现一次 。该路径 至少包含一个 节点，且不一定经过根节点。

路径和 是路径中各节点值的总和。

给你一个二叉树的根节点 root ，返回其 最大路径和 。
```
#### 思路
最大路径和可以是两个节点之间的距离之和，根据题目思考，我们在计算的过程中肯定需要使用到下层节点向上返回的结果，因此确定使用递归的方式，递归出口为root == null，即从叶子节点开始返回，
在返回的过程中，有以下几种情况：
左子树单链返回，右子树单链返回，左 + 根 + 右以及根节点单独返回。其中，只有左 + 根 + 右这种情况返回后，就无法继续向上返回，此时要判断并更新一次全局结果res，其余的都可以继续向上返回
判断。在判断左右单链时，需要与0进行比较，如果小于零，那就直接返回0。
```
class Solution {
    int res = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        helper(root);
        return res;
    }
    public int helper(TreeNode root){
        if(root == null)return 0;
        int left = Math.max(helper(root.left), 0);
        int right = Math.max(helper(root.right), 0);
        res = Math.max(res, root.val + left + right);
        return root.val + Math.max(left, right);
    }
}
```

