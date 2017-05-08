## 题目
Given a linked list, remove the nth node from the end of list and return its head.

For example,

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.

## 思路分析
该题主要是要移除倒数第N个元素

## 代码实现

``` javascript
var removeNthFromEnd = function(head, n) {
    if(head===null){
        return head;
    }
    var first = head;
    var len = 0;
    //耗时stupid
    while(head){
        len++;
        head = head.next;
    }
    head = first;
    if(n===len){
        head = head.next;
        return head;
    }
    for(var i = 0;i<len-n-1;i++) {
        head = head.next;
    }
    if(head.next.next){
        head.next = head.next.next;
    }else{
        head.next = null;
    }
    return first;
};
```
这段代码的运行时间是159ms，只击败了22.5%，现在让我们Post
上另外一段运行时间是119ms的代码，来看看有什么区别

``` javascript
var removeNthFromEnd = function(head, n) {
    var p1 = head,p2 = head
    while (n-- > 0) {
        p1 = p1.next
    }
    //此处是标记
    if (p1 == null) {
        return head.next
    }
    //program
    while (p1.next != null) {
        p1 = p1.next
        p2 = p2.next
    }
    if (p2.next.next == null) {
        p2.next = null
    } else {
        p2.next = p2.next.next
    }    
    return head;
};
```
对比起上面的代码，此代码并没有去遍历整条链表来获得该链表的长度，先通过两个辅助变量来进行计算，p1先走n步，然后p2再开始起步等到p1走到尽头时，p2刚好走到要删除的那个元素前。其实program以后的代码的思路就是：`p2 = linklist.length - p1走过的长度`
