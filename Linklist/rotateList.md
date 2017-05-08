## 题目
Given a list, rotate the list to the right by k places, where k is non-negative.

For example:
Given 1->2->3->4->5->NULL and k = 2,
return 4->5->1->2->3->NULL.

## 思路分析
注意这里rotate的k是可以超过链表总数的，故k = k%link.length;

## 代码实现
``` javascript
var rotateRight = function(head, k) {
    if(head===null||head.next===null)
        return head;
    var last = head,
        lastHead = last,
        first = head,
        firstHead = first,
        count = 0,
        count1 = 0;
    //count the linklist's length
    while(first!==null) {
        first = first.next;
        count1++;
    }

    if(count1<=k){
        if(k%count1===0)
            return head;
        else
            k = k%count1;
    }

    while(last!==null&&last.next!==null) {
        if(count1-count-1===k) {
            first = last.next;
            firstHead = first;
            last.next = null;
            break;
        }
        last = last.next;
        count++;
    }
    while(first!==null&&first.next!==null)
        first = first.next;
    first.next = lastHead;

    head = firstHead;
    return head;    
};
```
---
## 想法
然而这并不是最佳的做法，不过我感觉最佳的做法思路和我差不多，限于本人的资历，没看出到底那里运行速度比我的快，希望大神指教

## 最佳代码
``` javascript
var rotateRight = function(head, k) {
    //scan through the list & put them in a hash map for fast look up later <key, node>
    //remember previous node's key
    if(head===null){return head;}
    var copy = head;
    var dummy = new ListNode(-1);
    dummy.next = head;
    var i=1;

    //count the length of the list
    while(head.next !== null){
        head = head.next;
        i++;
    }

    k=k % i;
    if(k=== 0){
        return dummy.next;
    }
    //console.log("k is "+k +" i is "+i);

    head = dummy.next;
    var old_head = dummy.next;
    for(var a = 0; a< i-k-1;a++){
        head = head.next;
    }
    //console.log(head.val);
    dummy.next= head.next;
    head.next = null;
    head = dummy.next;
    while(head.next!==null){
        head=head.next;
    }
    head.next = old_head;

    return dummy.next;
};
```
