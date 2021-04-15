# 打家劫舍II

> 这个题我记得以前用C语言写过，还是半年前暑假的时候，现在又蹦出来了，着实看不懂题库

* 这个题目是典型的动态规划的题目，当前的状态只需要看前两格的状态即可，也不需要输出最佳的解决方案，只需要求出最大的值就行了
* 这个问题的核心在于怎么隔离首尾相连的情况：
  * 当我们使用第一个元素的时候，我们可以限制最后一个元素必然不能使用，当我们不使用第一个元素的时候，即第二个元素为开头，那么最后一个元素也没有了使用的限制
  * 这两种情况比较大小就可以得出来了
  * 把算最大值的程序封装成一个函数，使用start和length作为数组访问的界限即可

```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length==1){
            return nums[0];
        }
        int val1 = getMax(nums,0,nums.length-1);
        int val2 = getMax(nums,1,nums.length-1);//第二个元素开始计算
        return val1>val2?val1:val2;

    }
    private int getMax(int [] nums,int start,int len){
        int stolen[] = new int[len+1];
        int max = 0;
        stolen[0] = 0;
        stolen[1]=nums[0+start];
        for(int i=2;i<len+1;i++){
            stolen[i] = stolen[i-1]>stolen[i-2]+nums[i-1+start]? stolen[i-1]:stolen[i-2]+nums[i-1+start];
        }
        return stolen[len];
    }
}
```

