两个用链表表示的整数，每个结点包含一个数位。这些数位是反向存放的，也就是个位排在链表的首部。编写函数对这两个整数求和，并用链表形式返回结果。
给定两个链表ListNode* A，ListNode* B，请返回A+B的结果(ListNode*)。

```java
import java.util.*;
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
// 循环
public class Plus {
    public ListNode plusAB(ListNode a, ListNode b) {
        int sum = 0, num = 0, up = 0;
        ListNode head = null, cur = null;
        while (a != null || b != null) {
            int aVal = 0, bVal = 0;
            if (a != null) {
                aVal = a.val;
            }
            if (b != null) {
                bVal = b.val;
            }
            sum = aVal + bVal + up;
            num = sum % 10;
            up = sum / 10;
            if (a != null) {
                a = a.next;
            }
            if (b != null) {
                b = b.next;
            }
            ListNode node = new ListNode(num);
            if (head == null) {
                head = node;
                cur = node;
            }else {
                cur.next = node;
                cur = node;
            }
        }
        if (up != 0) {
            ListNode node = new ListNode(up);
            cur.next = node;
        }
        return head;
    }
}
```
```java
// 递归
import java.util.*;
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Plus {
    public ListNode plusAB(ListNode a, ListNode b) {
        int up = 0;
        return addList(a, b, up);
    }
    public ListNode addList(ListNode a, ListNode b, int up) {
        if (a == null && b == null && up == 0)
            return null;
        int value = up;
        if (a != null) {
            value += a.val;
        }
        if (b != null) {
            value += b.val;
        }
        ListNode result = new ListNode(value%10);
        ListNode more = addList(a == null ? null : a.next, b == null ? null : b.next, value/10);
        result.next = more;
        return result;
    }
}
```
另一种情况：所有数位正向存放
```java
import java.util.*;

public class Plus {
    private class ListNode {
        int val;
        ListNode next = null;
        ListNode prev = null;

        ListNode(int val) {
            this.val = val;
        }
    }
    private class PartialSum {
        ListNode sum = null;
        int carry = 0;
    }
    public int length(ListNode l) {
        int len = 0;
        while (l != null) {
            ++len;
            l = l.next;
        }
        return len;
    }
    public ListNode addList(ListNode a, ListNode b) {
        int len1 = length(a);
        int len2 = length(b);
        // 对较短链表进行补零
        if (len1 < len2) {
            a = padList(a, len2-len1);
        }else {
            b = padList(b, len1-len2);
        }
        // 对两个链表求和
        PartialSum sum = addListsHelper(a, b);
        // 判断是否有进位
        if (sum.carry == 0) {
            return sum.sum;
        }else {
            ListNode result = inserBefore(sum.sum, sum.carry);
            return result;
        }
    }
    public ListNode padList(ListNode l, int padding) {
        ListNode head = l;
        for (int i=0; i<padding; i++) {
            ListNode n = new ListNode(0);
            head.prev = n;
            n.next = head;
            head = n;
        }
        return head;
    }
    public PartialSum addListsHelper(ListNode a, ListNode b) {
        if (a == null && b == null)
            return new PartialSum();
        PartialSum sum = addListsHelper(a.next, b.next);
        int value = a.val+b.val+sum.carry;
        ListNode result = inserBefore(sum.sum, value%10);
        sum.sum = result;
        sum.carry = value/10;
        return sum;
    }
    public ListNode inserBefore(ListNode l, int value) {
        ListNode n = new ListNode(value);
        if (l != null) {
            l.prev = n;
            n.next = l;
        }
        return n;
    }
}

```
