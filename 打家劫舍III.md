# 打家劫舍III

* 这个题目是一个树状结构的递归问题，但是因为涉及到状态转移（父节点需要做出选择），所以可以称为动态规划的题目

* 难点在哪呢?

  * 我们需要区分两种状态，这里我是用的条件语句进行划分，很多题解的内容是使用一个标签位来表示,1代表选中，0代表没有被选中的情况
  * 怎么优化:仔细观察一下，一个节点会被访问两次，被他父节点访问一次，得到父节点的输出，第二次被爷爷节点访问，得到爷爷节点的输出，**此后上层的树节点就跟他没有关系了！**
    * 我们可以建立一张hash表，这样防止了重复计算数节点
    * 但是我的算法不能跑完所有测试样例😂，看完题解后推断是每个节点都加入了一个hashamp这样咋get()的时候会很耗时间

* 官方题解怎么做?

  * 用两个hashmap!分别存放根节点选中和不选中的最大值，我的那个hashmap把这两个融合到了一起，不是一个很好的策略
  * 基本思路是一样的g(0) = max{f(l),g(l)}+max{f(r),g(r)}

* 看到了一个很厉害民间题解，采用数组的方式解释:

  * 因为这个问题有无后效性的概念

  * 分析：（这里略过暴力解法和记忆化递归。）

    根据打家劫舍 I 和 II，我们有了经验，这是一个动态规划问题；
    问题场景在「树」上，就要用到「树的遍历」，这里用「后序遍历」，这是因为：我们的逻辑是子结点陆续汇报信息给父结点，一层一层向上汇报，最后在根结点汇总值。
    关键：当前结点「偷」或者「不偷」决定了孩子结点偷或者不偷，把这一点设计成状态，放在第 2 维，这一步叫「消除后效性」，这一点技巧非常常见。

    第 1 步：状态定义
    dp[node][j] ：这里 node 表示一个结点，以 node 为根结点的树，并且规定了 node 是否偷取能够获得的最大价值。

    j = 0 表示 node 结点不偷取；
    j = 1 表示 node 结点偷取。
    第 2 步： 推导状态转移方程
    根据当前结点偷或者不偷，就决定了需要从哪些子结点里的对应的状态转移过来。

    如果当前结点不偷，左右子结点偷或者不偷都行，选最大者；
    如果当前结点偷，左右子结点均不能偷。
    （状态转移方程的表述有点复杂，请大家直接看代码。）

    第 3 步： 初始化
    一个结点都没有，空节点，返回 0，对应后序遍历时候的递归终止条件；

    第 4 步： 输出
    在根结点的时候，返回两个状态的较大者。

    第 5 步： 思考优化空间
    优化不了。

    参考代码：

    Java

    public class Solution {

        // 树的后序遍历
        
        public int rob(TreeNode root) {
            int[] res = dfs(root);
            return Math.max(res[0], res[1]);
        }
        
        private int[] dfs(TreeNode node) {
            if (node == null) {
                return new int[]{0, 0};
            }
        
            // 分类讨论的标准是：当前结点偷或者不偷
            // 由于需要后序遍历，所以先计算左右子结点，然后计算当前结点的状态值
            int[] left = dfs(node.left);
            int[] right = dfs(node.right);
        
            // dp[0]：以当前 node 为根结点的子树能够偷取的最大价值，规定 node 结点不偷
            // dp[1]：以当前 node 为根结点的子树能够偷取的最大价值，规定 node 结点偷
            int[] dp = new int[2];
        
            dp[0] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
            dp[1] = node.val + left[0] + right[0];
            return dp;
        }
    }

* 我写的解题方法:

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    Map<TreeNode,Integer> map = new HashMap<TreeNode,Integer>();
    public int rob(TreeNode root) {
//用hashmap记录节点处的的最大返回值，因为每个节点要参与两次最大值的生成
//构建函数返回以root为根的最大返回值
//动态规划的关系,root返回的最大值有两种情况:1.偷本节点+孙子节点最大值和 2. 不偷本节点+儿子节点最大值和
//思路先放在这里，明天来写
        return getMax(root);
    }
    private int getMax(TreeNode root){
        if(map.containsKey(root)){
            return map.get(root);
        }
        else{
            if(root==null){
                return 0;
            }
            int val1 = root.val ;
            if(root.left!=null){
                val1+=rob(root.left.left)+rob(root.left.right);
            }
            if(root.right!=null){
                val1+=rob(root.right.left)+rob(root.right.right);
            }
            int val2 = rob(root.left)+rob(root.right);
            return Math.max(val1,val2);
        }
    }
}
```




