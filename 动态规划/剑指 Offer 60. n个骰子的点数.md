### [剑指 Offer 60. n个骰子的点数](https://leetcode.cn/problems/nge-tou-zi-de-dian-shu-lcof/)

把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率。

你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。

 

**示例 1:**
>输入: 1
输出: [0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]

**示例 2:**
>输入: 2
输出: [0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13889,0.11111,0.08333,0.05556,0.02778]
 

**限制：**
1 <= n <= 11

参考题解：[【n个骰子的点数】：详解动态规划及其优化方式](https://leetcode.cn/problems/nge-tou-zi-de-dian-shu-lcof/solution/nge-tou-zi-de-dian-shu-dong-tai-gui-hua-ji-qi-yo-3/)

> 比较关键的两步，一步是“dp[j] = 0;”，一步是“if (j - cur < i-1)”。对于前一步，因为是从后往前逐个累加，在加到当前点数时，必须把原先存放的n-1个骰子的数据置0，否则累加出错。对于后一步，如果不加此判据，会取到n-2个骰子的数据，此时可认为是“脏数据”，会导致累加出错。从实际情况来分析，n-1个骰子的最小值就是n-1，不会比这再小，因此此处的判据是 i-1，而不是0；

```java
public class DicesProbability {
    public double[] dicesProbability(int n){
        int[] dp = new int[70];
        for (int i = 0; i <= 6; i++) {
            dp[i] = 1;
        }
        for (int i = 2; i <= n; i++) {
            for (int j = 6 * i; j >= i; j--) {
                dp[j] = 0;
                for (int k = 1; k <= 6; k++) {
                    if (j - k < i - 1){
                        break;
                    }
                    dp[j] += dp[j - k];
                }
            }
        }
        int all = (int) Math.pow(6, n);
        double[] res = new double[5 * n + 1];
        for (int i = n; i <= 6 * n; i++) {
            res[i - n] = dp[i] * 1.0 / all;
        }
        return res;
    }
}
```