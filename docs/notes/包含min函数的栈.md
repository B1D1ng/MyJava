# 题目
>定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。
>注意：保证测试中不会当栈为空的时候，对栈调用pop()或者min()或者top()方法。
# 思路
首先我们定义一个栈用来存储元素，并且在对栈push的时候我们可以设置一个最小值变量min进行比较和更新，但是当我们pop的时候，如果将最小值元素pop出去了，如何更新最小值呢？此时我们应该发现，只定义一个栈是不能满足题目要求的，那么我们可以创建第二个栈用来存储最小元素，当有新元素入栈时，与最小值进行比较，如果比当前最小值小，那就同时将这个新的最小值push进最小元素栈中即可。
# 代码
```
import java.util.Stack;
public class Solution {
    private Stack<Integer> stack = new Stack<>();
    private Stack<Integer> stack1 = new Stack<>();
    private int min = 0;
    private int top = 0;
    public void push(int node) {
        if(stack.empty()){
            min = node;
            stack1.push(min);
        }
        else if(node<min){
                min = node;
                stack1.push(min);
            }
        stack.push(node);
       }
    
    public void pop() {
        if(stack.empty()){
            return;
        }
        int pop = stack.pop();
        if(pop==min){
             stack1.pop();
             min = stack1.pop();
             stack1.push(min);
        }
    }
    public int top() {
        int top = stack.pop();
        stack.push(top);
        return top;
    }
    
    public int min() {
        return min;
    }
}
```
>运行时间：15ms,占用内存：9448k
