题目: 链表中倒数第k个结点

题目描述： 输入一个链表，输出该链表中倒数第k个结点

JS
```
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function FindKthToTail(head, k)
{
    if (!head || k<=0)
        return null;
    var p = head,
        q = head;
    // 怎么找临界点？？
	for (var i=0;i<k-1;i++) {
		if (p.next) {
			p = p.next;
        }else {
            return null;
        }
    }
    for (;p.next;p=p.next) {
        q = q.next;
    }
    return q;
}
module.exports = {
    FindKthToTail : FindKthToTail
};
```

Java
```

```
