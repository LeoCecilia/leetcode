## 题目
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You must do this in-place without altering the nodes' values.

For example,
Given {1,2,3,4}, reorder it to {1,4,2,3}.

## 思路分析
先将链表分成两半，然后将后半部分逆序，最后再将两个部分分别链接起来

## 代码实现
``` javascript
var reorderList = function(head) {
    if(head===null||head.next===null)
        return;
    var slow = head,
        fast = head;

    //find middle
    while(fast.next!==null&&fast.next.next!==null){
        slow = slow.next;
        fast = fast.next.next;
    }

    //reverse the half after the middle
    function reverse(head) {
        if(head===null||head.next === null) {
            return head;
        }
        var node = reverse(head.next);
        head.next.next = head;
        head.next = null;
        return node;
    }

    //这里只需要一条链表，不需要两条链表
    var p2 = reverse(slow.next);
    slow.next = p2;
  	var p1 = head;
  	p2 = slow.next;
  	while(p1!==slow){
  		slow.next = p2.next;
      //用slow.next保存p2.next，而不是用slow来保存
  		p2.next = p1.next;
  		p1.next = p2;
  		p1 = p2.next;//相当于p1 = p1.next;
  		p2 = slow.next;
  	}
};
```
