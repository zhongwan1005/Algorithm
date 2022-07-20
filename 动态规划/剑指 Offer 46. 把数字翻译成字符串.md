### [剑指 Offer 46. 把数字翻译成字符串](https://leetcode.cn/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

给定一个数字，我们按照如下规则把它翻译为字符串：`0` 翻译成 `“a”` ，`1` 翻译成 `“b”`，……，`11` 翻译成 `“l”`，……，`25` 翻译成 `“z”`。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

**示例 1:**

> 输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
 
思路类似于 **斐波那契数列和青蛙爬楼梯**，只是多了判定条件

其中 dp[i]表示以数字x结尾有多少种表示方法

```java
class Solution {
    public int translateNum(int num) {
        String str = Integer.toString(num);
        int len = str.length();
        int a =1, b = 1;
        for (int i = 2; i <= len; i++){
            String tmp = str.substring(i - 2, i);
            int c = 0;
            if (tmp.compareTo("10") >= 0 && tmp.compareTo("25") <= 0){
                c = a + b;
            }
            else{
                c = b;
            }
            a = b;
            b = c;
        }
        return b;
    }
}
```