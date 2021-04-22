# 矩形区域不超过K的最大数值和

> 这个题目我想到了mmnn复杂度的解法，在某个维度上使用有序集合可以化简为logn的方法

```java
class Solution {
public int maxSumSubmatrix(int[][] matrix, int k) {
    int rows = matrix.length, cols = matrix[0].length, max = Integer.MIN_VALUE;
    // O(cols ^ 2 * rows)
    for (int l = 0; l < cols; l++) { // 枚举左边界
        int[] rowSum = new int[rows]; // 左边界改变才算区域的重新开始
        for (int r = l; r < cols; r++) { // 枚举右边界
            for (int i = 0; i < rows; i++) { // 按每一行累计到 dp
                rowSum[i] += matrix[i][r];
            }

            // 求 rowSum 连续子数组 的 和
            // 和 尽量大，但不大于 k
            max = Math.max(max, dpmax(rowSum, k));
        }
    }
    return max;
}

// 在数组 arr 中，求不超过 k 的最大值
private int dpmax(int[] arr, int k) {
    int max = Integer.MIN_VALUE;
    int temp=0;
    TreeSet<Integer> tree = new TreeSet<Integer>();
    for(int i =0;i<arr.length;i++){
        temp+=arr[i];
        tree.add(temp);
        Integer j =tree.ceiling(temp-k);
        if(j!= null){
            max=Math.max(temp-j,max);
        }
    }
    return max;
}
}
```

