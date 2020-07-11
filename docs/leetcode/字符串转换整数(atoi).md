# 题目
>请你来实现一个 atoi 函数，使其能将字符串转换成整数。<br/>
>首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。接下来的转化规则如下：<br/>
>1.如果第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字字符组合起来，形成一个有符号整数。<br/>
>2.假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成一个整数。<br/>
>3.该字符串在有效的整数部分之后也可能会存在多余的字符，那么这些字符可以被忽略，它们对函数不应该造成影响。<br/>
>注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换，即无法进行有效转换。<br/>
>在任何情况下，若函数不能进行有效的转换时，请返回 0 。<br/>
本题中的空白字符只包括空格字符 ' ' 。
假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 [−231,  231 − 1]。如果数值超过这个范围，请返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。

# 代码
```
class Solution {
    public int myAtoi(String str) {
        int[] range = {-1,-1};
        if(str == ""){
            return 0;
        }
        char[] c = str.toCharArray();
        StringBuilder sb = new StringBuilder();
        int i = 0;
        while(i < c.length){
            //获取第一个非空字符
            if(c[i] == ' '){
                i++;
            }
            else{
                break;
            }
        }
        //如果为空字符串，返回0
        if(i == c.length){
            return 0;
        }
        //如果不是非空字符串，则会找到第一个非空字符
        //如果第一个字符是负号或者数字
        if(c[i] == '-' || c[i] == '+' || (c[i]>='0' && c[i]<='9')){
             range[0] = i;
            i++;
            //如果是数字的话
            while(i < c.length && c[i]>='0' && c[i]<='9'){
                i++;
                if(i == c.length){
                    break;
                }
            }
            range[1] = i;
            String s = str.substring(range[0],range[1]);
            try{
                Integer result = Integer.parseInt(s);
                return result;
            }
            catch(Exception e){
                if((s.charAt(0) == '-' || s.charAt(0) == '+') && s.length() == 1){
                    return 0;
                }
                if(s.charAt(0) == '-'){
                    return -2147483648;
                }
                return 2147483647;
            }
        }
        return 0;
    }
}
```
# 总结
本题主要考察代码的鲁棒性，是否考虑到了各种测试用例。
