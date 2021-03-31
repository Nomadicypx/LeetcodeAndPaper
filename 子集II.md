# 子集II

* 做这个题的时候我没有先做子集I，是直接开始做的
* 首先开始的时候我没有看懂题意，直接采用高中数学的方法，每个元素有取和不取两个状态，直接递归到函数底部，即n==-1的时候生成一个list并且塞入到最终的结果当中
* 但是题目中会出现重复的元素，这会造成子集重复，如何解决重复问题？
  * 首先容易想到需要一个排序，这样能够吧重复的元素放到一起，有利于后续程序的编写，而不需要做多余的判断之类的
  * 设想一个元素前面的元素与自己值相同，那我是取还是不取呢？取的情况是可以的，这样是生成一个唯一子集的方式，相当于树往下延伸了一层，不取的时候是在树的同一层，我们要考虑现在这个结果是否以前就生成过了
    * 当前面这个元素不取的时候，我们现在这个元素应该也是不取的，因为前面不取说明一个唯一子集已经生成了
    * 当前面元素取的时候，我们应该是取或者不取都行，这样就相当于生成了一个子集

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {//先排个序
        //2^n次方进行元素的生成，生成完成后输送给生成函数生成数组插入到List中
        int len = nums.length;
        Arrays.sort(nums);
        boolean []window = new boolean[len];
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        generateIndex(len-1,nums,window,result);
        return result;
    }
    private void generateIndex(int n,int[]input,boolean[] window,List<List<Integer>>result){
        if(n==-1){
            List<Integer> list = new ArrayList();
            for(int i=0;i<window.length;i++){
                if(window[i]==true){
                    list.add(input[i]);
                }
            }
            result.add(list);
        }
        else{
            if(n==input.length-1){
                window[n]=true;
                generateIndex(n-1,input,window,result);
                window[n]=false;
                generateIndex(n-1,input,window,result);
            }
            else{
                if(window[n+1]==false&&input[n+1]==input[n]){
                    window[n]=false; 
                    generateIndex(n-1,input,window,result);
                }
                else{
                    window[n]=true;
                    generateIndex(n-1,input,window,result);
                    window[n]=false;
                    generateIndex(n-1,input,window,result);                    
                }
            }
        }
    }

}
```

