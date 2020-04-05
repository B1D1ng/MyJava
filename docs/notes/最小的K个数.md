# 题目
>输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。
# 思路
这道题的思路和找一个数组里的第K大（小）的思路类似，直接用堆排序即可，实践复杂度为O(nlogk)
# 代码
```
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] arr, int k) {
        ArrayList<Integer> arr1 = new ArrayList<>();
        if(k>arr.length){
            return arr1;
        }
        //建立小顶堆
        for(int i = arr.length/2-1;i>=0;i--){
            heapAdjust(arr,i,arr.length);
        }
        for(int j = arr.length-1;j>=arr.length-k;j--){
            arr1.add(arr[0]);
            int t = arr[0];
            arr[0] = arr[j];
            arr[j] = t;
            heapAdjust(arr,0,j);
        }
        return arr1;
    }
    public static void heapAdjust(int[] arr,int i,int len){
        int k = i;
        int temp = arr[k];
        int index = 2*k+1;
        while(index<len){
            if(index+1<len){
                if(arr[index]>arr[index+1]){
                    index++;
                }
            }
            if(temp>arr[index]){
                arr[k] = arr[index];
                k = index;
                index = 2*k+1;
            }
            else{
                break;
            }
        }
        arr[k] = temp;
    }
}
```
>运行时间：18ms,占用内存：9468k
