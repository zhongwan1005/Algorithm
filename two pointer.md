### [31. 下一个排列](https://leetcode.cn/problems/next-permutation/)

整数数组的一个 **排列**  就是将其所有成员以序列或线性顺序排列。

- 例如，`arr = [1,2,3] `，以下这些都可以视作` arr `的排列：`[1,2,3]、[1,3,2]、[3,1,2]、[2,3,1] 。`

整数数组的 **下一个排列** 是指其整数的下一个字典序更大的排列。更正式地，如果数组的所有排列根据其字典顺序从小到大排列在一个容器中，那么数组的** 下一个排列 **就是在这个有序容器中排在它后面的那个排列。如果不存在下一个更大的排列，那么这个数组必须重排为字典序最小的排列（即，其元素按升序排列）。

- 例如，`arr = [1,2,3]` 的下一个排列是` [1,3,2]` 。
- 类似地，`arr = [2,3,1] `的下一个排列是 `[3,1,2] `。
- 而 `arr = [3,2,1] `的下一个排列是 `[1,2,3] `，因为` [3,2,1] `不存在一个字典序更大的排列。

给你一个整数数组 `nums` ，找出` nums `的下一个排列

必须**原地**修改，只允许使用额外常数空间。



**示例 1：**

> 输入:nums = [1,2,3]
输出：[1,3,2]

**示例 2：**

> 输入：nums = [3,2,1]
输出：[1,2,3]

**示例 3：**

> 输入：nums = [1,1,5]
输出：[1,5,1]

```java
class NextPermutation {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]){
            i--;
        }
        if (i >= 0){
            int j = nums.length - 1;
            while (j >= 0 && nums[i] >= nums[j]){
                j--;
            }
            swap(nums, i, j);
        }
        reverse(nums, i + 1, nums.length - 1);
    }

    private void reverse(int[] nums, int left, int right) {
        while (left < right){
            swap(nums, left++, right--);
        }
    }

    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```


### [556. 下一个更大元素 III](https://leetcode.cn/problems/next-greater-element-iii/)

给你一个正整数 `n` ，请你找出符合条件的最小整数，其由重新排列 `n` 中存在的每位数字组成，并且其值大于 `n` 。如果不存在这样的正整数，则返回 `-1` 。

**注意** ，返回的整数应当是一个 **32 位整数** ，如果存在满足题意的答案，但不是 **32 位整数** ，同样返回 `-1` 。

**示例 1：**
>输入：n = 12
输出：21

**示例 2：**
>输入：n = 21
输出：-1

```java
public class NextGreaterElement {
    public int nextGreaterElement(int n) {
        char[] nums = Integer.toString(n).toCharArray();
        int i = nums.length - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]){
            i--;
        }
        if (i < 0){
            return -1;
        }

        int j = nums.length - 1;
        while (j >= 0 && nums[i] >= nums[j]){
            j--;
        }
        swap(nums, i, j);
        reverse(nums, i + 1, nums.length - 1);
        long ans = Long.parseLong(new String(nums));
        return ans > Integer.MAX_VALUE ? -1 : (int)ans;
    }
    
    private void reverse(char[] nums, int left, int right) {
        while (left < right){
            swap(nums, left++, right--);
        }
    }

    private void swap(char[] nums, int i, int j) {
        char tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

```py
class NextGreaterElement:
    def nextGreaterElement(self, n: int) -> int:
        nums = list(str(n))
        i = len(nums) - 2
        while i >= 0 and nums[i] > nums[i + 1]:
            i -= 1
        if i < 0:
            return -1

        j = len(nums) - 1
        while j >= 0 and nums[i] > nums[j]:
            j -= 1
        nums[i], nums[j] = nums[j], nums[i]
        # left, right = i + 1, len(nums) - 1
        # while left < right:
        #     nums[left], nums[right] = nums[right], nums[left]
        #     left += 1
        #     right -= 1
        nums[i + 1:] = nums[i + 1:][::-1]
        res = int(''.join(nums))
        return res if res < 2 ** 31 else -1
```