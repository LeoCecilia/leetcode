## 题目
Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

## 思路分析
这次代码的实现我通过画图来能更好地了解如何去操作链表。
## 代码实现
``` javascript
var swapPairs = function(head) {
    if(!head||!head.next)
        return head;
    var dunny = new ListNode(-1);
    dunny.next = head;

    var dunny2 = dunny,
        p,
        p1;

    while(dunny2.next&&dunny2.next.next){
        p = dunny2.next;
        p1 = dunny2.next.next;
        p.next = p1.next;
        p1.next = dunny2.next;
        dunny2.next = p1;
        dunny2 = dunny2.next.next;
    }

    return dunny.next;
};
```
## 更佳的代码（递归）
其实链表本就是递归的数据结构，所以用递归来操作链表再合适不过了。
``` javascript
//递归
var swapPairs = function(head) {
    const n1 = head;
    if (!n1) { return null; }

    const n2 = n1.next;

    if (n2) {
        n1.next = swapPairs(n2.next);
        n2.next = n1;
        return n2;
    } else {
        return n1;
    }
};
//我写的

```
