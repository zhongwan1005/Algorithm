### [剑指 Offer 14- I. 剪绳子](https://leetcode.cn/problems/jian-sheng-zi-lcof/)

给你一根长度为 `n` 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m-1]` 。请问 `k[0]*k[1]*...*k[m-1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

**示例 1：**

>输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1

**示例 2:**

>输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36

解法1：动态规划
参考题解：[剑指 Offer 14- I. 剪绳子，还是动态规划好理解，但是贪心真的快](https://leetcode.cn/problems/jian-sheng-zi-lcof/solution/jian-zhi-offer-14-i-jian-sheng-zi-huan-s-xopj/)

```java
class Solution {
    public int cuttingRope(int n) {
        int[] dp = new int[n + 1];
        dp[2] = 1;
        for (int i = 3; i <= n; i++){
            for (int j = 2; j < i; j++){
                dp[i] = Math.max(dp[i], Math.max(j * (i - j), j * dp[i - j]));
            }
        }
        return dp[n];
    }
}
```

解法2：贪心
证明参考：[面试题14- I. 剪绳子（数学推导 / 贪心思想，清晰图解）](https://leetcode.cn/problems/jian-sheng-zi-lcof/solution/mian-shi-ti-14-i-jian-sheng-zi-tan-xin-si-xiang-by/)
```java
class Solution {
    public int cuttingRope(int n) {
        if (n <= 3){
            return n - 1;
        }
        int a = n / 3, b = n % 3;
        if (b == 0){
            return (int)Math.pow(3, a);
        }
        else if(b == 1){
            return (int)Math.pow(3, a - 1) * 4;
        }
        return (int)Math.pow(3, a) * 2;
    }
}
```