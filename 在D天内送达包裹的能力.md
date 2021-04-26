# 在D天内送达包裹的能力

> 这个问题我开始以为是动态规划，后来感觉是贪心，然后看到了需要装入连续的包裹，那么就不存在最优解了，模拟就可以求出天数，遍历即可，题解采用二分查找

算法

```java
class Solution {
    public int shipWithinDays(int[] weights, int D) {
        int sum =0;
        int max=Integer.MIN_VALUE;
        for(int i=0;i<weights.length;i++){
            max = Math.max(max,weights[i]);
            sum+=weights[i];
        }
        int arr[] = new int[sum-max+1];
        for(int i=0;i<arr.length;i++){
            arr[i]=getDays(weights,max+i);   
            if(arr[i]<=D){
                return max+i;
            }
        }
        return-1;
    }
    public int getDays(int [] weights, int volumn){
        int leftVolumn = 0;
        int count = 0 ;
        for(int i=0;i<weights.length;i++){
            if(leftVolumn<weights[i]){
                leftVolumn = volumn-weights[i];         
                count+=1;
            }
            else{
                leftVolumn = leftVolumn-weights[i];
    
            }
        }
        return count;
    }
}
```

