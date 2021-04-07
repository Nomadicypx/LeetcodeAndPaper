# 搜索旋转排序数组II

* 排序的数组找值，那肯定是二分呀，但题目恶心在它截断了一个数组，那么单纯的二分就有点子没办法了，搜索旋转排序数组I里头是根据端点的值来判断是否有序的，而II里存在重复的元素，题解是怎么调整的呢？
  * 基本算法是一样的，还是二分，但是对于端点相等的情况，有可能端点相同，那就不知道该往哪边去了，因为哪边对你来说都是一样的，所以针对相等的情况要做特殊的处理
  * 题解里头处理为左右指针分别++和--
* 我是怎么解这个题的呢？
  * 遍历一遍！哈哈结果时间还是100%简直离谱

> 官方题解

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int n = nums.length;
        if (n == 0) {
            return false;
        }
        if (n == 1) {
            return nums[0] == target;
        }
        int l = 0, r = n - 1;
        while (l <= r) {
            int mid = (l + r) / 2;
            if (nums[mid] == target) {
                return true;
            }
            if (nums[l] == nums[mid] && nums[mid] == nums[r]) {
                ++l;
                --r;
            } else if (nums[l] <= nums[mid]) {
                if (nums[l] <= target && target < nums[mid]) {
                    r = mid - 1;
                } else {
                    l = mid + 1;
                }
            } else {
                if (nums[mid] < target && target <= nums[n - 1]) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
        }
        return false;
    }
}

```

