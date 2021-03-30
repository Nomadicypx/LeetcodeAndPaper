# 删除链表的倒数第N个节点

* 注意边界条件，当head==null的情况，删除的元素是第一个元素的情况
* 扫两遍，第一遍确定位置，第二遍删除元素

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if(head==null){
            return null;
        }
        int len =0;
        ListNode cur = head;
        while(cur!=null){
            len++;
            cur = cur.next;
        }
        if(n==len){
            return head.next;
        }
        ListNode pre = new ListNode(0,head);
        cur = head;
        int count = 1;
        
        while(count<len-n+1&&cur!=null){
            pre= cur;
            cur=cur.next;
            count++;
        }
        pre.next = cur.next;
        return head;
    }
}
```

