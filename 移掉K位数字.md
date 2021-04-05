# 移掉K位数字

* 这个题目我看完想了一下，想到了一个跟题解差不多的思路，采用栈来进行增序排序，但是没有题解想得那么细致，导致很多细节问题需要调试
* 需要注意的细节:
  * 当栈顶元素大于手上的元素的时候肯定是需要添加元素进栈的，但是存在一些问题
    * 当已经弹出了K个元素的时候肯定就不需要进栈了
    * 所以循环终止的条件应该是弹出K个元素
  * 当栈顶元素小于手上的元素的时候怎么办？
    * 元素直接压入栈
  * 栈的意义：我们可以用一个栈维护当前的答案序列，栈中的元素代表截止到当前位置，删除不超过 k*k* 次个数字后，所能得到的最小整数
  * 但是到数组走完，可能存在没有满足K个元素剔除
    * 如果我们删除了 mm 个数字且 m<km<k，这种情况下我们需要从序列尾部删除额外的 k-mk−m 个数字。
    * 如果最终的数字序列存在前导零，我们要删去前导零。
    * 如果最终数字序列为空，我们应该返回 00。

```java
class Solution {
    public String removeKdigits(String num, int k) {
        int len = num.length();
        if(len==k){
            return "0";
        }
        Deque<Character> deque = new LinkedList<Character>();
        //用双端队列好一些，一边队列模拟栈操作，一头作为最后出栈的出口
        //栈顶元素大于数组元素且栈中元素与数组剩余元素的和大于最后的长度即可
        int count = 0;//记录弹出栈顶的元素的个数
        int scount = 0;//记录栈中的元素
        int i =0;
        while(i<len){
            if(deque.isEmpty()){
                deque.addFirst(num.charAt(i++));
                scount++;            
            }
            else{
                if(deque.peekFirst()>num.charAt(i)){
                    deque.removeFirst();                   
                    count++;
                    scount--;
                }
                else{
                    deque.addFirst(num.charAt(i));  
                    scount++;                  
                    i++;
                }
            }
            if(count>=k){
                break;
            }
        }
        
        while(scount>len-k){
            deque.removeFirst();
            scount--;
        }
        while(i<len){
            deque.addFirst(num.charAt(i));
            i++;
            scount++;
        }
        //输出
        StringBuffer buf = new StringBuffer();
        while(!deque.isEmpty()){
            char c = deque.removeLast();
            buf.append(c);
        }
        String res = buf.toString();
        int reslen = res.length();
        int result = 0;
        for(int j=0;<reslen;j++){
            int val = res.charAt(i)-'0';
            result = result*10+val;
        }
        return String.valueOf(result);
    }

}
```

* 上面这个我没写完，但感觉思路是对的，还需要调试，先放着

