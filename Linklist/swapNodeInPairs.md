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
