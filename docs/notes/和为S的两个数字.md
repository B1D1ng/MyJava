# 题目
>输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，将乘积最小的一对数字存入列表中返回。
# 思路一：
这道题的可以按照leetcode第一题两数之和的方式来解，实践复杂度为O(n),空间复杂度为O(n)
```
public class Solution {
    public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
        HashMap<Integer,Integer> hm = new HashMap<>();
        ArrayList<Integer> arr = new ArrayList<>();
        for(int i = 0;i<array.length;i++){
            if(hm.containsValue(sum-array[i])){
                if(arr.size()==0){
                    if(array[i]<sum-array[i]){
                        arr.add(array[i]);
                        arr.add(sum-array[i]);
                    }
                    else{
                        arr.add(sum-array[i]);
                        arr.add(array[i]);
                    }
                }
                else {
                    int oldmul = arr.get(0) * arr.get(1);
                    int newmul = array[i] * (sum-array[i]);
                    if(newmul<oldmul){
                        if(array[i]<sum-array[i]){
                        arr.set(0,array[i]);
                        arr.set(1,sum-array[i]);
                        }
                        else{
                             arr.set(1,array[i]);
                             arr.set(0,sum-array[i]);
                        }
                    }
                }
            }
            else{
                hm.put(array[i],array[i]);
            }
        }
        return arr;
     }
}
>运行时间：14ms，占用内存：9284k
# 思路2
我们还没有利用到所给数组有序的特性，接下来我们思考一下能否根据这个特性将空间复杂度降为O(1)。其实分析一下这个递增数组，可以看出，找到的第一对数字就是乘积最小的数字对。
# 代码
```
public class Solution {
    public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
    ArrayList<Integer> result = new ArrayList<Integer>();
        if(array.length<=1) return result;
        int i=0,j=array.length-1;
        while(i<j){
            if(array[i]+array[j]<sum){
                i++;
                continue;
            }
            if(array[i]+array[j]>sum){
                j--;
                continue;
            }
            result.add(array[i]);
            result.add(array[j]);
            break;
        }
        return result;
    }
}
>运行时间：16ms,占用内存：9300k
