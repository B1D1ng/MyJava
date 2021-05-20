# 题目
```
输入一个字符串，打印出该字符串中字符的所有排列。

 

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

 

示例:

输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
 

限制：

1 <= s 的长度 <= 8
```
# 思路
DFS+回溯+剪枝，剪枝需要先将原字符数组进行排序，从而出现重复字符排列在一起
# 代码
```
class Solution {
    public String[] permutation(String s) {
        List<String> lists = new ArrayList<>();
        boolean[] visited = new boolean[s.length()];
        char[] chars = s.toCharArray();
        Arrays.sort(chars);
        dfs(chars, lists, visited, new StringBuilder());
        return lists.toArray(new String[lists.size()]);
    }
    public void dfs(char[] chars, List<String> lists, boolean[] visited, StringBuilder sb){
        if(sb.length() == chars.length){
            lists.add(sb.toString());
            return;
        }
        for(int i = 0; i < chars.length; i++){
            if(visited[i] == true || i > 0 && chars[i] == chars[i - 1] && visited[i - 1] == false)continue;
            sb.append(chars[i]);
            visited[i] = true;
            dfs(chars, lists, visited, sb);
            visited[i] = false;
            sb.deleteCharAt(sb.length()-1);
        }
    }
}
```
