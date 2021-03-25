# 删除排序链表中的重复元素II

* 这个垃圾题目看着简单，结果还是写了好久！
* 倒不是思路的问题，是有几个指针的先后调整顺序理了好久
* 有一个坑是函数的输入是一个node节点，里头是有有意义的值的！！所以一个数组如果开头就是重复的数字就难搞了，我就是在这个点上卡了很久

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode fixpre = new ListNode();
        fixpre.next = head;
        ListNode pre = fixpre;
        ListNode cur = head;
        while(cur!=null){
            boolean flag = testDuplicates(cur);
            if(flag){
                int i =0;
                while(testDuplicates(cur)){
                    cur=cur.next;                   
                    i++;
                }
                System.out.println(i);
                cur = cur.next;
                pre.next = cur;
            }
            else{
                pre.next = cur;
                pre = cur;
                cur = cur.next;
            }
        }
        return fixpre.next;
    }
    private boolean testDuplicates(ListNode point){
        if(point==null||point.next==null){
            return false;//与后面一个元素没有重复
        }
        if(point.val==point.next.val){
            return true;
        }
        else{
            return false;
        }
    }
}
```

