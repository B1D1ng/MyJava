#### 题目
```
给定一个二叉树和一个值\ sum sum，判断是否有从根节点到叶子节点的节点值之和等于\ sum sum 的路径
```
#### 思路
典型递归解法，当位于叶子节点并且和值等于目标值时，返回true，位于null时返回false，其余情况继续递归
```
public class Solution {
    /**
     * 
     * @param root TreeNode类 
     * @param sum int整型 
     * @return bool布尔型
     */
    public boolean hasPathSum (TreeNode root, int sum) {
        // write code here
        if(root == null)return false;
        return dfs(root, sum);
    }
    public boolean dfs(TreeNode node, int target){
        if(node == null)return false;
        if(node.left == null && node.right == null && target == node.val)return true;
        return dfs(node.left, target - node.val) || dfs(node.right, target - node.val);
    }
}
```
