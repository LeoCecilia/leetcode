## 题目
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

Example:

Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7

## 题目解释
实现链表的加法，且不能使用逆序方法，由于可以使用js数组的堆栈，(先进后出的方法)来实现

## 代码实现
``` javascript
var addTwoNumbers = function(l1, l2) {
    var a1 = [],
        a2 = [],
        list = new ListNode(0),
        sum = 0;
    while(l1){
        a1.push(l1.val);
        l1 = l1.next;
    }
    while(l2){
        a2.push(l2.val);
        l2 = l2.next;
    }
    while(a1.length||a2.length){
        if(a1.length)
            sum+=a1.pop();
        if(a2.length)
            sum+=a2.pop();
        //这里是为了减少后面的0判断
        var head = new ListNode(Math.floor(sum/10));
        list.val = sum%10;
        head.next = list;
        list = head;
        sum = Math.floor(sum/10);
    }
    return list.val===0?list.next:list;
};
```
