### [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

统计一个数字在**排序数组**中出现的次数。

 
**示例 1:**

> 输入: nums = [5,7,7,8,8,10], target = 8
输出: 2

**示例 2:**

> 输入: nums = [5,7,7,8,8,10], target = 6
输出: 0

**tips:** 经典二分，在有重复元素的排序数组中查找某个元素的左右边界

```java
class Solution {
    public int search(int[] nums, int target) {
        return binSearch(nums, target) - binSearch(nums, target - 1);
    }

    //查找右边界
    private int binSearch(int[] nums, int target){
        int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] <= target){
                left = mid + 1;
            }
            else {
                right = mid - 1;
            }
        }
        return left;
    }
}
```