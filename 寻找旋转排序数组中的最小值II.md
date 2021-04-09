# 寻找旋转排序数组中的最小值II

> 这个题目是昨天做过的那道题目的变形，出现重复值的情况需要考虑相等时数值的处理

* 做二分查找一定要确定最小值所在的范围，否则会遗漏，我开始自己写的解法只是简单地正确处理了大于和小于的情况 而等于的情形没有考虑取值的范围问题，把最小值遗漏了
* 下面粘贴一段别人的题解，其中对最小值处在的范围进行了解析
* 设置 leftleft, rightright 指针在 numsnums 数组两端，midmid 为每次二分的中点：
  * 当 nums[mid] > nums[right]时，midmid 一定在第 1 个排序数组中，ii 一定满足 mid < i <= right，因此执行 left = mid + 1；
  * 当 nums[mid] < nums[right] 时，midmid 一定在第 2 个排序数组中，ii 一定满足 left < i <= mid，因此执行 right = mid；
  * 当 nums[mid] == nums[right] 时，是此题对比 153题 的难点（原因是此题中数组的元素可重复，难以判断分界点 ii 指针区间）；
    * 例如 [1, 0, 1, 1, 1][1,0,1,1,1] 和 [1, 1, 1, 0, 1][1,1,1,0,1] ，在 left = 0, right = 4, mid = 2 时，无法判断 midmid 在哪个排序数组中。
    * 我们采用 right = right - 1 解决此问题，证明：
      此操作不会使数组越界：因为迭代条件保证了 right > left >= 0；
      此操作不会使最小值丢失：假设 nums[right]nums[right] 是最小值，有两种情况：
      若 nums[right]nums[right] 是唯一最小值：那就不可能满足判断条件 nums[mid] == nums[right]，因为 mid < right（left != right 且 mid = (left + right) // 2 向下取整）；
      若 nums[right]nums[right] 不是唯一最小值，由于 mid < right 而 nums[mid] == nums[right]，即还有最小值存在于 [left, right - 1][left,right−1] 区间，因此不会丢失最小值。

```java

class Solution {
    public int findMin(int[] nums) {
        int len = nums.length;
        if(len==1||nums[0]<nums[len-1]){
            return nums[0];
        }
        int low = 0;
        int high = nums.length - 1;
        while (low < high) {
            int pivot = (low+high) / 2;
            if (nums[pivot] < nums[high]) {
                high = pivot;
            } else if (nums[pivot] > nums[high]) {
                low = pivot + 1;
            } else {
                high -= 1;
            }
        }
        return nums[low];
    }
}

```

* 上面这个是官方题解，下面这个是我写的

```java
class Solution {
    public int findMin(int[] nums) {
//二分法解决，但是可能存在一个问题，当l和mid对应的值相等的时候应该怎么办？
//问题的核心在于我们的终止条件是什么——当mid和l相等的时候
//那么怎么逼近呢？
        int len = nums.length;
        if(len==1||nums[0]<nums[len-1]){
            return nums[0];
        }
        else{
            //若l 和 r相等的时候我们干脆让r=r-1
            int l = 0;
            int r = len-1;
            int mid = (l+r)/2;
            while(l<r){
                if(nums[l]<nums[mid]){
                    l = mid+1;
                    mid = (l+r)/2;
                }
                else if(nums[l]>nums[mid]){
                    r = mid;
                    mid = (l+r)/2;
                }
                else{
                    r = r-1;
                    mid = (r+l)/2;
                }
            }

            return nums[l];
        }
    }
}
```





