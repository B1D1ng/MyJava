# 题目
>输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序
# 思路一：暴力法
核心公式就是(首项+末项)*项数/2 = S，暴力双层循环即可
# 代码
```
public class Solution {
    public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
        ArrayList<ArrayList<Integer>> arr = new ArrayList<>();
       for(int i = 1;i<=sum;i++){
           for(int j = i+1;j<=sum;j++){
               if((i+j)*(j-i+1)==2*sum){
                   ArrayList<Integer>arr1 = new ArrayList<>();
                   for(int m = i;m<=j;m++){
                       arr1.add(m);
                   }
                   arr.add(arr1);
               }
           }
       }
        return arr;
    }
}
```
# 思路二：滑动窗口
我们可以设置两个指针：首项和末项，首项从1开始，末项从2开始，如果(front+rear)*(rear-front+1)<2*S的话，则把尾指针后移，如果相等则存储并且移动任意一个指针。如果
(front+rear)*(rear-front+1)>2*S则移动首指针，结束条件为当front走到数列的一半时
# 代码
```
public class Solution {
    public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
        ArrayList<ArrayList<Integer>> arr = new ArrayList<>();
        int front = 1;
        int rear = 2;
       while(front<sum/2+1){
           if((front+rear)*(rear-front+1)<2*sum){
               rear++;
           }
           else if((front+rear)*(rear-front+1)==2*sum){
               ArrayList<Integer> arr1 = new ArrayList<>();
               for(int i = front;i<=rear;i++){
                   arr1.add(i);
               }
               arr.add(arr1);
               front++;
           }
           else front++;
       }
        return arr;
    }
}
```
>运行时间：18ms,占用内存：9648k
