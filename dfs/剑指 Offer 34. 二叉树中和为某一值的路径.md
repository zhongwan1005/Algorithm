### [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode.cn/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

给你二叉树的根节点 `root `和一个整数目标和` targetSum` ，找出所有 **从根节点到叶子节点** 路径总和等于给定目标和的路径。

**叶子节点** 是指没有子节点的节点。

**示例 1：**

![剑指offer34pathsumii1](../pic/剑指offer34pathsumii1.jpg)

> 输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[ [5,4,11,2],[5,8,4,5] ]

**示例 2：**

> 输入：root = [1,2,3], targetSum = 5
输出：[]

**示例 3：**

> 输入：root = [1,2], targetSum = 0
输出：[]

---

***为啥path需要add和remove, 而sum最后不需要 sum+=root.val?***
> 因为我们这里用的是递归，也就是当递归到头的时候会回溯。所以`target`和`path`不同，`path`是只有一个，每次递归都是直接在操作（改变）`path`里的值；但是`target`是每次递归都有自己的`target`，所以递归到头，回溯到上一级，`target`指的是上一级的`target`。故不需要对`target`做操作。可能有一点绕，但是意思其实就是：`path`只有一个，`target`则是每次递归都有自己的`target`。



```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int target) {
        if (root == null){
            return new ArrayList<>();
        }
        List<List<Integer>> res = new ArrayList<>();
        Deque<Integer> path = new ArrayDeque<>();
        dfs(root, target, path, res);
        return res;
    }

    private void dfs(TreeNode root, int target, Deque<Integer> path, List<List<Integer>> res){
        if (root == null){
            return;
        }
        path.add(root.val);
        target -= root.val;
        System.out.println("before: " + path + ", " + target);
        //target减为0, 并且为叶子结点
        if (target == 0 && root.left == null && root.right == null){
            res.add(new ArrayList<>(path));
        }
        dfs(root.left, target, path, res);
        dfs(root.right, target, path, res);        
        path.removeLast(); 
        System.out.println("after: " + path + ", " + target);       
    }
}
```