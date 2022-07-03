### [剑指 Offer 62. 圆圈中最后剩下的数字](https://leetcode.cn/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。

**示例 1：**

> **输入:** n = 5, m = 3
**输出:** 3

**示例 2：**

> **输入:** n = 10, m = 17
**输出:** 2

数学方法参考此篇题解: [换个角度举例解决约瑟夫环](https://leetcode.cn/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/solution/huan-ge-jiao-du-ju-li-jie-jue-yue-se-fu-huan-by-as/)


![约瑟夫环复原](pic/约瑟夫环.png)
```Java
//链表模拟
class Solution {
    public int lastRemaining(int n, int m) {
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            list.add(i);
        }
        int index = 0;
        while (n > 1){
            index = (index + m - 1) % n;
            list.remove(index);
            n--;
        }
        return list.get(0);
    }
}    

```



```Python
# python模拟超时
class LastRemaining:
    def lastRemaining(self, n: int, m: int) -> int:
        circle = [i for i in range(n)]
        
        index = 0
        while n > 1:
            index = (index + m - 1) % n
            circle.pop(index)
            n -= 1
        return circle[0]

# 数学方法
class Solution:
    def lastRemaining(self, n: int, m: int) -> int:
        ans = 0
        for i in range(2, n + 1):
            ans = (ans + m) % i
        return ans

```