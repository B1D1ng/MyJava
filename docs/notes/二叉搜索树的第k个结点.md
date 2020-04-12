# 题目
>给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。
# 思路
题目给的是二叉搜索树，按中序遍历返回第k个结点即可
# 代码
```
import java.util.*;
public class Solution {
    TreeNode KthNode(TreeNode pRoot, int k)
    {    
       if(pRoot==null)return null;
        ArrayList<TreeNode> arr = new ArrayList<>();
        InOrder(pRoot,arr);
        if(k<=0||k>arr.size())return null;
        return arr.get(k-1);
    }
    void InOrder(TreeNode pRoot,ArrayList<TreeNode> arr){
        if(pRoot!=null){
            InOrder(pRoot.left,arr);
            arr.add(pRoot);
            InOrder(pRoot.right,arr);
        }
    }
}
```
>运行时间：30ms,占用内存：9816k


#拓展题目
>给定一棵二叉树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。
# 思路
如果给定的是乱序的二叉树，那么按中序遍历则无法得到有序的结点，需要先创建数组列表按层序遍历存储二叉树的结点，再按堆排序的方式得到topk
# 代码
```
import java.util.*;
public class Solution {
    TreeNode KthNode(TreeNode pRoot, int k)
    {    
       if(pRoot==null){
           return null;
       }
       ArrayList<TreeNode> arr = new ArrayList<>();
        arr.add(pRoot);
        int i = 0;
        while(i<arr.size()){
            if(arr.get(i).left!=null)arr.add(arr.get(i).left);
            if(arr.get(i).right!=null)arr.add(arr.get(i).right);
            i++;
        }
        if(k<=0||k>arr.size())return null;
        //创建初始小顶堆
        for(int i1 = arr.size()/2-1;i1>=0;i1--){
            headAdjust(arr,i1,arr.size());
        }
        //调整堆
        for(int j = arr.size()-1;j>arr.size()-k;j--){
            TreeNode t = arr.get(j);
            arr.set(j,arr.get(0));
            arr.set(0,t);
            headAdjust(arr,0,j);
        }
        return arr.get(0);
    }
    void headAdjust(ArrayList<TreeNode> arr,int i,int len){
        int k = i;
        int index = 2*k+1;
        TreeNode t = arr.get(i);
        while(index < len){
            if(index+1<len){
                if(arr.get(index).val>arr.get(index+1).val){
                    index++;
                }
            }
            if(t.val > arr.get(index).val){
                arr.set(k,arr.get(index));
                k = index;
                index = 2*k+1;
            }
            else{
                break;
            }
        }
        arr.set(k,t);
    }
}
```
