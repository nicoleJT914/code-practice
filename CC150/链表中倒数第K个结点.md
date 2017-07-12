输入一个链表，输出该链表中倒数第k个结点。

**注意边界条件的判断！**
```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        if (head == null || k<=0)
            return null;
        ListNode cur = head;
        ListNode pre = head;
        for (int i=0; i<k-1; i++) {
            if (cur.next != null) {
                cur = cur.next;
            } else {
                return null;
            }
        }
        while (cur.next != null) {
            cur = cur.next;
            pre = pre.next;
        }
        return pre;
    }
}
```
