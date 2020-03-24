# 题目
>输入一个链表，输出该链表中倒数第k个结点。
# 思路一
看到题目，首先最容易想到的方法应该是先遍历一次链表，得到链表的总的结点数，再得到倒数第K个结点。
```
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        //空链表
            if(head==null){
                return null;
            }
        int count = 0;
        ListNode p = head;
         while(true){
             if(p!=null){
                 count++;
                 p = p.next;
             }
             else{
                 break;
             }
         }
        if(count<k){
            return null;
        }
        p = head;
        for(int i = 0;i < count - k;i++){
            p = p.next;
        }
        return p;
    }
}
```
>运行时间：22ms,占用内存：9400k,时间复杂度为O(n)，空间复杂度为O(1)
