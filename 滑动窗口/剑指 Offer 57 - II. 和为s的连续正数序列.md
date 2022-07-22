### [剑指 Offer 57 - II. 和为s的连续正数序列](https://leetcode.cn/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

输入一个正整数 `target` ，输出所有和为 `target` 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

 

**示例 1：**

> 输入：target = 9
输出：[ [2,3,4], [4,5] ]

**示例 2：**

> 输入：target = 15
输出：[ [1,2,3,4,5], [4,5,6], [7,8] ]

**tips:**返回值为二维数组，初始化时可将返回值定义为`List<int[]> ans`

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        List<int[]> ans = new ArrayList<>();
        int i = 1, j = 1;
        int sum = 0;
        while (j <= target){
            if (sum < target){
                sum += j;
                j++;
            }
            else if (sum > target){
                sum -= i;
                i++;
            }
            else {
                int[] tmp = new int[j - i];
                for (int k = i; k < j; k++){
                    tmp[k - i] = k;
                }
                ans.add(tmp);
                sum -= i;
                i++;
            }
        }
        
        int[][] res = new int[ans.size()][];
        return ans.toArray(res);
    }
}
```