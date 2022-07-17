### [剑指 Offer 38. 字符串的排列](https://leetcode.cn/problems/zi-fu-chuan-de-pai-lie-lcof)


输入一个字符串，打印出该字符串中字符的所有排列。

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

 

**示例:**

> 输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]



```java
class Solution {
    public String[] permutation(String s) {
        char[] chs = s.toCharArray();
        boolean[] visited = new boolean[chs.length];
        List<String> list = new ArrayList<>();
        StringBuilder path = new StringBuilder();
        //排序是剪枝的前提
        Arrays.sort(chs);
        dfs(chs, visited, 0, path, list);

        String[] res = new String[list.size()];
        for (int i = 0; i < list.size(); i++){
            res[i] = list.get(i);
        }
        return res;
    }

    private void dfs(char[] chs, boolean[] visited, int index, StringBuilder path, List<String> list){
        if (index == chs.length){
            list.add(new String(path));
        }
        for (int i = 0; i < chs.length; i++){
            if (!visited[i]){
                //剪枝
                if (i > 0 && chs[i] == chs[i - 1] && visited[i - 1] == false){
                    continue;
                }

                path.append(chs[i]);
                visited[i] = true;
                
                dfs(chs, visited, index + 1, path, list);
  
                path.deleteCharAt(path.length() - 1);
                visited[i] = false;
                
            }
        }
    }
}
```