# 组合总和IV

> 今天看到这个题我是直接懵逼的，因为首先我觉得计算出总和为一个target的一个组合就很困难，其次这还是一个排列的问题

* 事实上如果只是一个组合的问题，那么这个问题就是一个完全背包的问题，每个元素可以无限的使用，如果是一个排列的问题那么就不太适用了，我们需要记录一下组合的长度，来乘以一个组合变成排列的因子，但是背包问题是以某个元素是否参与到组合中来进行的，这样组合的长度就不是增量的(不能通过i来表示)，不能满足DP的无后效性和增量特性（或者可以增加一个DP空间存放长度变量）
* 上面的想法很麻烦，所以我们需要直接使用排列的方法
* 定义状态dp[j]为总和为j的排列总数，那么dp[j+num[i]]和dp[j]的关系我门是能预料到的，即排列的最后一个元素为num[i]，那么我们求dp[target]呢？
  * dp[target] = dp[traget-nums[0]]+ dp[traget-nums[1]]+....

算法:

```java
class Solution {
    public int combinationSum4(int[] nums, int target) {
        Arrays.sort(nums);
        int dp[] = new int [target+1];
        dp[0] =1 ;
        for(int i=1;i<target+1;i++){
            for(int num:nums){
                if(i<num) break;
                else{
                    dp[i]+=dp[i-num];
                }
            }
        }
        return dp[target];

    }
}
```

