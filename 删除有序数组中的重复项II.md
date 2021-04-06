# 删除有序数组中的重复项II

> 这个题目希望能留下两个重复数字在数组里头，那么就要判断当前元素和之前的两个元素是否相等，相等就可以不可以添加进去，不相等就可以

* 初看这道题，肯定是快慢指针
* 有需要注意的是选择结构情况的合并，我写这道题，头脑不清晰，写了很多重复的内容和没有合并的地方，导致代码有些冗长
* 其次需要把判断是否相等的模块放到末尾，这样循环的头部可以只需要决定要不要放入元素了
* 需要注意当数组长度只为1或者2的时候，这个时候pre和prepre是不存在的，需要调整元素的值
* 我写的题解复杂度有点高，需要看题解

```java
class Solution {
    public int removeDuplicates(int[] nums) {
//快慢指针即可
        int fast = 0;
        int slow = 0;
        int pre = 100000;
        int prepre = 100000;
        int len = nums.length;
        int count = 0;
        boolean flag = true;
        for(;fast<len;){
            if(fast<2){
                if(fast==0){
                    nums[slow] = nums[fast];
                    slow++;
                    count++;           
                }
                if(fast==1){
                    nums[slow] = nums[fast];
                    slow++;
                    count++;
                }
            }
            else{
                if(flag==true){
                    nums[slow] = nums[fast];
                    slow++;
                    count++;
                }
            }
            prepre = pre;
            pre = nums[fast];
            fast++;
            if(fast<len&&nums[fast]==pre&&nums[fast]==prepre){
                flag = false;
            }
            else{
                flag = true;
            }
        }
        return count;
    }
}
```

* 化简版本在下面，思路理清楚很快就写出来了（5分钟）

```java
class Solution {
    public int removeDuplicates(int[] nums) {
//快慢指针即可
        int fast = 0;
        int slow = 0;
        int pre = 100000;
        int prepre = 100000;
        int len = nums.length;
        int count = 0;
        boolean flag = true;
        for(;fast<len;){
            if(flag==true){
                nums[slow]=nums[fast];
                slow++;
                count++;
            }
            prepre = pre;
            pre = nums[fast];
            fast++;
            if(fast<len&&nums[fast]==pre&&nums[fast]==prepre){
                flag = false;
            }
            else{
                flag = true;
            }
        }
        return count;
    }
}
```

