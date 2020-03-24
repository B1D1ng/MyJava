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
       int count = 1;
        ListNode p = head;
         while(true){
             if(p.next!=null){
                 p = p.next;
                 count++;
             }
             else{
                 break;
             }
         }
        //边界条件
        if(count<k||k<0){
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
# 思路二
思路一的方法是最通用的方法，但还是用到了两次循环，能否只用一次循环就能够得到想要返回的结点呢？
可以用双指针的方式，设置前指针pre和后指针last。
<br首先考虑边界情况，例如空链表，k<=0的情况。之后双指针的思想是，先让pre指针走到正序第k个位置，下一次移动时启动last指针同时移动，当pre指针走到最后一个结点时，last指针指向的结点就是倒数第k个结点。但注意！这里还存在一种边界条件，就是k等于count时，last指针不需要移动，k大于count时，越界。
```
import java.util.*;
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        //空链表
            if(head==null){
                return null;
            }
             if(k<=0){
            return null;    
            }
               //双指针法
            ListNode pre = head;
            ListNode last = head;
            int count = 1;
            while(pre.next!=null){
                pre = pre.next;
                count++;
                if(count>k){
                    last = last.next;
                }
            }
            if(count<k){
            return null;    
            }
            else{
                return last;
            }
    }
}
```
>运行时间：21ms,占用内存：9684k
