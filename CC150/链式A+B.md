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
