# 32 - III. 从上到下打印二叉树 III

[力扣题目链接](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)


# 初见思路

## 基本思路(层序遍历)

使用一个变量`layer`来记录层序遍历的层数（从`1`开始），如果`layer`为偶数，则需要将保存当前层结点的`ArrayList`集合进行翻转

## 边界问题

如果`root`为`null`，直接返回空的结果集合

## Java代码
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null){
            return res;
        }

        Queue<TreeNode> queue = new ArrayDeque<>();
        int layer = 1;
        
        queue.offer(root);
        while (!queue.isEmpty()){
            int curSize = queue.size();
            List<Integer> list = new ArrayList<>();
            TreeNode parent = null;
            for (int i = 0; i < curSize; i++){
                parent = queue.poll();
                list.add(parent.val);
                if (parent.left != null){
                    queue.offer(parent.left);
                }
                if (parent.right != null){
                    queue.offer(parent.right);
                }
            }
            if (layer % 2 == 0){
                Collections.reverse(list);
            }
            res.add(list);
            layer++;
        }
        return res;
    }
}
```

## 复杂度分析
- 时间复杂度：$O(N)$，其中$N$为二叉树的结点个数，每个结点恰好被遍历一次
- 空间复杂度：$O(N)$，最坏的情况是二叉树只有一边的子节点形成了链表，递归栈需要消耗$O(N)$的空间